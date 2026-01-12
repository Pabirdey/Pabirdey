<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <!-- ================= REQUIRED CSS ================= -->
    <!-- Bootstrap 4 (datepicker compatible) -->
    <link rel="stylesheet"
          href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css">

    <!-- Bootstrap Datepicker -->
    <link rel="stylesheet"
          href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css">

    <!-- ================= REQUIRED JS ================= -->
    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

    <!-- Bootstrap 4 JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js"></script>

    <!-- Datepicker JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

    <style>
        body {
            font-family: Courier New, Courier, monospace;
        }

        .Main-Heading {
            font-size: 40px;
            font-weight: bold;
            text-align: center;
            margin: 20px;
        }

        .form-group-box {
            border: 3px solid #73AD21;
            padding: 15px;
            border-radius: 15px;
            width: 520px;
            margin-bottom: 20px;
        }

        th {
            background: #343a40;
            color: white;
            font-size: 14px;
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
            background: #e9ecef;
            text-align: center;
            cursor: pointer;
        }

        .list-box {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #999;
            z-index: 999;
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

    <!-- ================= DATE + FURNACE ================= -->
    <div class="form-group-box">
        <label style="font-size:22px;">Date :</label>
        <input id="tbFDatePick"
               class="form-control d-inline-block"
               style="width:150px;text-align:center"
               readonly>

        <label class="ml-4" style="font-size:22px;">Furnace :</label>
        <select id="lstFur" class="form-control d-inline-block" style="width:80px;">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <!-- ================= MUDGUN TABLE ================= -->
    <div class="table-responsive" style="max-height:300px;">
        <table class="table table-bordered table-sm text-center" id="Mudgun_Details">
            <thead>
            <tr>
                <th>Cast No</th>
                <th>Closure Mode</th>
                <th>Clay Used</th>
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

    $(document).ready(function () {

        // ================= DATEPICKER INIT =================
        $('#tbFDatePick').datepicker({
            format: 'dd/mm/yyyy',
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', new Date());

        lsSelectedFDate = $('#tbFDatePick').val();

        // ================= DATE CHANGE =================
        $('#tbFDatePick').on('changeDate', function () {
            lsSelectedFDate = $(this).val();
            loadMudgunData();
        });

        // ================= FURNACE CHANGE =================
        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();
            loadMudgunData();
        });

        loadMudgunData();
    });

    // ================= DUMMY DATA LOAD =================
    function loadMudgunData() {

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
                    <select class="form-control">
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
                <td><input class="form-control" value="${data[i].LOT_NO}"></td>
            </tr>`;
        }

        $("#Mudgun_Details tbody").html(html);
    }

    // ================= CUSTOM DROPDOWN =================
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
