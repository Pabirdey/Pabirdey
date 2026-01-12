<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <!-- ========== BOOTSTRAP 5 LATEST ========== -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- ========== JQUERY ========== -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

    <!-- ========== BOOTSTRAP JS ========== -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        body {
            font-family: Courier New, Courier, monospace;
        }

        .Main-Heading {
            font-size: 6vh;
            font-weight: bold;
            text-align: center;
            padding: 20px;
        }

        th {
            background: #343a40;
            color: white;
            font-size: 14px;
            position: sticky;
            top: 0;
            text-align: center;
        }

        .highlight td {
            background: yellow !important;
        }

        .input-wrapper {
            display: flex;
            border: 1px solid #999;
        }

        .input-wrapper input {
            border: none;
            outline: none;
            width: 100%;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #e9ecef;
        }

        .list-box {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #999;
            z-index: 9999;
            width: 100%;
        }

        .list-box div {
            padding: 5px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #f1f1f1;
        }
    </style>
</head>

<body>

<div class="Main-Heading">Cast House Details</div>

<div class="container-fluid">

    <!-- ========== DATE + FURNACE ========== -->
    <div class="border rounded p-3 mb-3" style="width:520px;">
        <label class="fw-bold fs-4">Date :</label>

        <!-- ✅ Native Date Picker -->
        <input type="date"
               id="tbFDatePick"
               class="form-control d-inline-block"
               style="width:180px;">

        <label class="fw-bold fs-4 ms-4">Furnace :</label>
        <select id="lstFur" class="form-select d-inline-block" style="width:90px;">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <!-- ========== MUDGUN DETAILS TABLE ========== -->
    <div class="table-responsive" style="max-height:320px;">
        <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
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

<script>
    let lsSelectedFDate = "";
    let IsSelectedFur = "C";

    // ========== PAGE LOAD ==========
    $(document).ready(function () {

        // Set today date
        let today = new Date().toISOString().split('T')[0];
        $("#tbFDatePick").val(today);
        lsSelectedFDate = today;

        $("#tbFDatePick").on("change", function () {
            lsSelectedFDate = $(this).val();
            loadMudgunData();
        });

        $("#lstFur").on("change", function () {
            IsSelectedFur = $(this).val();
            loadMudgunData();
        });

        loadMudgunData();
    });

    // ========== LOAD TABLE (DEMO / AJAX READY) ==========
    function loadMudgunData() {

        // Replace with AJAX response
        let data = [
            { CAST_NO: "101", CLOSURE_MODE: "MUDGUN", MG_CLAY_USED: "ACE", LOT_NO: "L001" },
            { CAST_NO: "102", CLOSURE_MODE: "NULL", MG_CLAY_USED: "BRL", LOT_NO: "L002" }
        ];

        let html = "";

        for (let i = 0; i < data.length; i++) {
            html += `
            <tr data-castno="${data[i].CAST_NO}">
                <td>${data[i].CAST_NO}</td>

                <td>
                    <select class="form-select">
                        <option></option>
                        <option ${data[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${data[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>

                <td style="position:relative;">
                    <div class="input-wrapper">
                        <input id="clayInput_${i}" value="${data[i].MG_CLAY_USED}">
                        <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                    </div>
                    <div class="list-box" id="list_${i}">
                        <div onclick="selectItem(this,${i})">ACE</div>
                        <div onclick="selectItem(this,${i})">BRL</div>
                        <div onclick="selectItem(this,${i})">LRH</div>
                        <div onclick="selectItem(this,${i})">OTHERS</div>
                    </div>
                </td>

                <td>
                    <input class="form-control" value="${data[i].LOT_NO}">
                </td>
            </tr>`;
        }

        $("#Mudgun_Details tbody").html(html);
    }

    // ========== CUSTOM DROPDOWN ==========
    function toggleList(index) {
        $("#list_" + index).toggle();
    }

    function selectItem(el, index) {
        $("#clayInput_" + index).val(el.innerText);
        $("#list_" + index).hide();

        if (el.innerText === "OTHERS") {
            alert("OTHERS selected at row " + index);
        }
    }

    // Close dropdown when clicking outside
    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper")) {
            document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");
        }
    });
</script>

</body>
</html>
