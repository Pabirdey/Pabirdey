<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
        }

        .header-box {
            background: #0d47a1;
            color: white;
            padding: 10px;
            border-radius: 10px;
        }

        .section-box {
            background: #1976d2;
            color: white;
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
        }

        .table input {
            width: 60px;
        }

        textarea {
            height: 120px;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">

    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4 class="m-0">FURNACE HIGH LINE LOG SHEET</h4>
        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>Shift A</option>
                <option>Shift B</option>
                <option>Shift C</option>
            </select>
        </div>
    </div>

    <!-- TABS -->
    <ul class="nav nav-tabs mt-3">
        <li class="nav-item">
            <a class="nav-link active" data-bs-toggle="tab" href="#tab1">Coke Unloading</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab2">High Line Log</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab3">Bin Position</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab4">Unloading Report</a>
        </li>
    </ul>

    <!-- TAB CONTENT -->
    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">

            <div class="row mt-2">

                <!-- LEFT TABLE -->
                <div class="col-md-6">
                    <div class="section-box">
                        <h6>Coke Unloading</h6>

                        <div class="table-responsive">
                            <table class="table table-bordered text-center bg-white">
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
                </div>

                <!-- RIGHT SIDE -->
                <div class="col-md-6">

                    <div class="row">

                        <!-- Others -->
                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Others</h6>

                                <label>Eastern Bunker</label>
                                <input class="form-control mb-2">

                                <label>Western Bunker</label>
                                <input class="form-control mb-2">

                                <label>Middle Bunker</label>
                                <input class="form-control mb-2">
                            </div>
                        </div>

                        <!-- Coke & Nut Coke -->
                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Coke & Nut Coke</h6>

                                <input class="form-control mb-2" placeholder="Material advised">
                                <input class="form-control mb-2" placeholder="Time advised">
                                <input class="form-control mb-2" placeholder="Material received">
                                <input class="form-control mb-2" placeholder="Time received">
                                <input class="form-control mb-2" placeholder="Unloaded">
                                <input class="form-control mb-2" placeholder="Loco left">
                                <input class="form-control mb-2" placeholder="Sent down">
                                <input class="form-control mb-2" placeholder="Total">
                            </div>
                        </div>

                    </div>

                    <!-- Remarks -->
                    <div class="section-box mt-2">
                        <h6>Remarks & Delays</h6>
                        <textarea class="form-control"></textarea>
                    </div>

                </div>

            </div>
        </div>

        <!-- OTHER TABS -->
        <div class="tab-pane fade" id="tab2">
            <h5 class="mt-3">High Line Log Content</h5>
        </div>

        <div class="tab-pane fade" id="tab3">
            <h5 class="mt-3">Bin Position Content</h5>
        </div>

        <div class="tab-pane fade" id="tab4">
            <h5 class="mt-3">Unloading Report Content</h5>
        </div>

    </div>

    <!-- FOOTER -->
    <div class="d-flex justify-content-end gap-2 mt-3">
        <button class="btn btn-success">Save</button>
        <button class="btn btn-danger">Delete</button>
        <button class="btn btn-secondary">Exit</button>
    </div>

</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<!-- JS FOR ROW GENERATION + TOTAL -->
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

    // Generate 5 rows
    for (let i = 0; i < 5; i++) {
        document.getElementById("tblBody").innerHTML += createRow();
    }

</script>

</body>
</html>