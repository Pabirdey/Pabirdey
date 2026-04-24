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
            font-weight: bold;
        }

        .header-box {
            background: #0d47a1;
            color: white;
            padding: 10px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }

        .section-box {
            background: #1976d2;
            color: white;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 10px;
        }

        .table-responsive {
            overflow-x: auto;
            max-height: 400px;
        }

        .table th, .table td {
            text-align: center;
            white-space: nowrap;
            font-size: 13px;
        }

        .table input, .table select {
            width: 100%;
            min-width: 60px;
            font-size: 12px;
            padding: 3px;
        }

        textarea {
            height: 80px;
        }

        .btn-custom {
            width: 120px;
            border-radius: 25px;
        }

        .material-name {
            background: #e3f2fd;
        }

    </style>
</head>

<body>

<div class="container-fluid mt-2">

    <!-- HEADER -->
    <div class="header-box">
        <h5 class="m-0">Furnace High Line Log Sheet</h5>

        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </div>
    </div>

    <!-- TABS -->
    <ul class="nav nav-tabs mt-3">
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

    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">

            <div class="row mt-2">

                <!-- LEFT -->
                <div class="col-lg-6 col-md-12">

                    <div class="section-box">
                        <h6>Coke Unloading</h6>

                        <div class="table-responsive">
                            <table class="table table-bordered bg-white">
                                <thead>
                                    <tr>
                                        <th>Date</th>
                                        <th>Shift</th>
                                        <th>Bunker</th>
                                        <th>C</th>
                                        <th>E</th>
                                        <th>F</th>
                                        <th>Total</th>
                                        <th>Position</th>
                                        <th>Balance</th>
                                    </tr>
                                </thead>
                                <tbody id="tblBody"></tbody>
                            </table>
                        </div>
                    </div>

                </div>

                <!-- RIGHT -->
                <div class="col-lg-6 col-md-12">

                    <div class="section-box">
                        <h6>Others</h6>
                        <input class="form-control mb-2" placeholder="Eastern">
                        <input class="form-control mb-2" placeholder="Western">
                        <input class="form-control mb-2" placeholder="Middle">
                    </div>

                    <div class="section-box">
                        <h6>Remarks</h6>
                        <textarea class="form-control"></textarea>
                    </div>

                </div>

            </div>
        </div>

        <!-- TAB 2 -->
        <div class="tab-pane fade" id="tab2">

            <div class="row mt-2">

                <div class="col-lg-8 col-md-12">
                    <div class="section-box">
                        <h6>High Line Log</h6>

                        <div class="table-responsive">
                            <table class="table table-bordered bg-white text-dark">
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
                                        <td><input></td>
                                        <td><input></td>
                                        <td><input></td>
                                        <td><input></td>
                                        <td><input></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <div class="col-lg-4 col-md-12">
                    <div class="section-box">
                        <h6>Remarks</h6>
                        <textarea class="form-control"></textarea>
                    </div>
                </div>

            </div>

        </div>

        <!-- TAB 3 -->
        <div class="tab-pane fade" id="tab3">

            <div class="section-box mt-2">

                <h6 class="text-center">Raw Material Position</h6>

                <div class="table-responsive">
                    <table class="table table-bordered bg-white">
                        <thead>
                            <tr>
                                <th>Material</th>
                                <th>Yard</th>
                                <th>H.L</th>
                                <th>Stock</th>
                                <th>C</th>
                                <th>E</th>
                                <th>F</th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr>
                                <td class="material-name">SINTER</td>
                                <td><input></td>
                                <td><input></td>
                                <td><input></td>
                                <td><input></td>
                                <td><input></td>
                                <td><input></td>
                            </tr>
                        </tbody>

                    </table>
                </div>

            </div>

        </div>

    </div>

</div>

<!-- JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>
function createRow() {
    return `
    <tr>
        <td><input type="date"></td>
        <td>
            <select>
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>
        <td><input></td>
        <td><input class="c" oninput="calcTotal(this)"></td>
        <td><input class="e" oninput="calcTotal(this)"></td>
        <td><input class="f" oninput="calcTotal(this)"></td>
        <td><input class="total" readonly></td>
        <td><input></td>
        <td><input></td>
    </tr>`;
}

function calcTotal(el) {
    let row = el.closest("tr");

    let c = parseFloat(row.querySelector(".c").value) || 0;
    let e = parseFloat(row.querySelector(".e").value) || 0;
    let f = parseFloat(row.querySelector(".f").value) || 0;

    row.querySelector(".total").value = c + e + f;
}

// generate rows
for (let i = 0; i < 5; i++) {
    document.getElementById("tblBody").innerHTML += createRow();
}
</script>

</body>
</html>