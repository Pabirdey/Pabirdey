<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
            font-family: Verdana;
            font-size: 13px;
        }

        .header-box {
            background: #0d47a1;
            color: white;
            padding: 8px;
            border-radius: 8px;
        }

        .header-box h4 {
            font-size: 18px;
        }

        .section-box {
            background: #1976d2;
            color: white;
            padding: 8px;
            border-radius: 8px;
            margin-top: 8px;
        }

        .section-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        /* TABLE */
        .table th {
            background: #1565c0;
            color: white;
            font-size: 12px;
            padding: 4px;
        }

        .table td {
            background: white;
            color: black;
            font-size: 12px;
            padding: 3px;
        }

        /* INPUT */
        .table input,
        .table select {
            width: 100%;
            font-size: 12px;
            padding: 2px;
            height: 28px;
            text-align: center;
        }

        textarea {
            height: 80px;
            font-size: 12px;
        }

        /* TABS */
        .nav-tabs .nav-link {
            font-size: 13px;
            padding: 5px 10px;
        }

        .btn-custom {
            width: 110px;
            border-radius: 20px;
            font-size: 12px;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-2">

    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4 class="m-0">Furnace High Line Log Sheet</h4>

        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control form-control-sm">
            <select class="form-select form-select-sm">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </div>
    </div>

    <!-- TABS -->
    <ul class="nav nav-tabs mt-2">
        <li class="nav-item">
            <a class="nav-link active" data-bs-toggle="tab" href="#tab1">Coke Unloading</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab2">HighLine Log</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab3">Bin Position</a>
        </li>
    </ul>

    <!-- TAB CONTENT -->
    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">
            <div class="row mt-2">

                <div class="col-md-8">
                    <div class="section-box">
                        <div class="section-title">Coke Unloading</div>

                        <table class="table table-bordered text-center">
                            <thead>
                                <tr>
                                    <th>Date</th>
                                    <th>Shift</th>
                                    <th>Bunker</th>
                                    <th>C-BF</th>
                                    <th>E-BF</th>
                                    <th>F-BF</th>
                                    <th>Total</th>
                                    <th>Position</th>
                                    <th>Balance</th>
                                </tr>
                            </thead>
                            <tbody id="tblBody"></tbody>
                        </table>
                    </div>
                </div>

                <div class="col-md-4">
                    <div class="section-box">
                        <div class="section-title">Remarks</div>
                        <textarea class="form-control"></textarea>
                    </div>
                </div>

            </div>
        </div>

        <!-- TAB 2 -->
        <div class="tab-pane fade" id="tab2">
            <div class="section-box mt-2">
                <div class="section-title">High Line Log</div>

                <table class="table table-bordered text-center">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Recd</th>
                            <th>Retd</th>
                            <th>Reason</th>
                            <th>U/L</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>LRP</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- TAB 3 -->
        <div class="tab-pane fade" id="tab3">
            <div class="section-box mt-2">
                <div class="section-title">Bin Position</div>

                <table class="table table-bordered text-center">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Yard</th>
                            <th>HL</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>SINTER</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </div>
</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>

function createRow() {
    return `
    <tr>
        <td><input type="date" class="form-control"></td>
        <td>
            <select class="form-control">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>
        <td><input class="form-control"></td>
        <td><input class="form-control c" oninput="calcTotal(this)"></td>
        <td><input class="form-control e" oninput="calcTotal(this)"></td>
        <td><input class="form-control f" oninput="calcTotal(this)"></td>
        <td><input class="form-control total" readonly></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
    </tr>`;
}

function calcTotal(el) {
    var row = el.closest("tr");

    var c = parseFloat(row.querySelector(".c").value) || 0;
    var e = parseFloat(row.querySelector(".e").value) || 0;
    var f = parseFloat(row.querySelector(".f").value) || 0;

    row.querySelector(".total").value = c + e + f;
}

// Generate rows
for (let i = 0; i < 5; i++) {
    document.getElementById("tblBody").innerHTML += createRow();
}

</script>

</body>
</html>
