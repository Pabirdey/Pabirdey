<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <!-- ================= CSS ================= -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker.min.css" rel="stylesheet">

    <style>
        body { font-family: Courier New, Courier, monospace; }

        .Main-Heading {
            font-size: 5vh;
            font-weight: bold;
            text-align: center;
            margin: 10px;
        }

        .scrollable-table { max-height: 320px; overflow-y: auto; }

        th {
            position: sticky;
            top: 0;
            background: #333;
            color: white;
            z-index: 2;
        }

        .datepicker {
            z-index: 9999 !important;
        }

        /* ===== Custom Dropdown ===== */
        .input-wrapper {
            display: flex;
            border: 1px solid #999;
            position: relative;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            border: 1px solid #999;
            background: white;
            display: none;
            max-height: 150px;
            overflow-y: auto;
            z-index: 999;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #e6e6e6;
        }
    </style>
</head>

<body>

<div class="Main-Heading">Cast House Details</div>

<div class="container-fluid">

    <!-- ================= DATE & FURNACE ================= -->
    <div class="mb-3">
        <label>Date:</label>
        <input type="text"
               id="tbFDatePick"
               class="form-control d-inline-block"
               style="width:150px;text-align:center;" />

        <label class="ms-3">Furnace:</label>
        <select id="lstFur" class="form-select d-inline-block" style="width:80px;">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
        </select>
    </div>

    <!-- ================= MUDGUN TABLE ================= -->
    <div class="scrollable-table">
        <table class="table table-bordered text-center align-middle" id="Mudgun_Details">
            <thead>
                <tr>
                    <th>Cast No</th>
                    <th>Closure Mode</th>
                    <th>MG Clay Type</th>
                    <th>Lot No</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>

</div>

<!-- ================= JS ================= -->
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>

<script>
$(document).ready(function () {

    var IsSelectedFur = $('#lstFur').val();
    var today = '@DateTime.Today.ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

    // ===== Datepicker =====
    $('#tbFDatePick').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    }).datepicker('setDate', today);

    // Initial Load
    Display_Mudgun_Details(today, IsSelectedFur);

    $('#tbFDatePick').on('changeDate', function () {
        Display_Mudgun_Details($(this).val(), IsSelectedFur);
    });

    $('#lstFur').change(function () {
        IsSelectedFur = $(this).val();
        Display_Mudgun_Details($('#tbFDatePick').val(), IsSelectedFur);
    });
});

// ================= AJAX LOAD =================
function Display_Mudgun_Details(Fdate, Fur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        dataType: 'json',
        data: { Fdate: Fdate, Fur: Fur },
        success: function (data) {

            var html = "";

            for (var i = 0; i < data.length; i++) {

                html += `<tr>
                    <td>${data[i].CAST_NO}</td>

                    <td>
                        <select class="form-select">
                            <option></option>
                            <option ${data[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                            <option ${data[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                        </select>
                    </td>

                    <td>
                        <div class="input-wrapper">
                            <input type="text" class="form-control"
                                   id="clayInput_${i}"
                                   value="${data[i].MG_CLAY_USED ?? ''}">
                            <div class="arrow-btn" onclick="toggleList(${i})">▼</div>

                            <div class="list-box" id="list_${i}">
                                <div onclick="selectItem(this,${i})">ACE</div>
                                <div onclick="selectItem(this,${i})">BRL</div>
                                <div onclick="selectItem(this,${i})">LRH</div>
                                <div onclick="selectItem(this,${i})">OTHERS</div>
                            </div>
                        </div>
                    </td>

                    <td>
                        <input class="form-control" value="${data[i].LOT_NO ?? ''}">
                    </td>
                </tr>`;
            }

            $("#Mudgun_Details tbody").html(html);
        }
    });
}

// ================= CUSTOM DROPDOWN =================
function toggleList(index) {
    closeAllLists();
    document.getElementById("list_" + index).style.display = "block";
}

function selectItem(el, index) {
    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    if (el.innerText === "OTHERS") {
        alert("Open modal here");
    }
}

function closeAllLists() {
    document.querySelectorAll(".list-box").forEach(function (l) {
        l.style.display = "none";
    });
}

document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper")) {
        closeAllLists();
    }
});
</script>

</body>
</html>