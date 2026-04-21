<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
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

        .small-input {
            width: 100%;
        }

        textarea {
            height: 150px;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">

    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4>FURNACE HIGH LINE LOG SHEET</h4>

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
        <li class="nav-item"><a class="nav-link active">Coke Unloading</a></li>
        <li class="nav-item"><a class="nav-link">High Line Log</a></li>
        <li class="nav-item"><a class="nav-link">Bin Position</a></li>
        <li class="nav-item"><a class="nav-link">Unloading Report</a></li>
    </ul>

    <!-- MAIN SECTION -->
    <div class="row">

        <!-- LEFT SIDE -->
        <div class="col-md-8">

            <!-- Coke Unloading -->
            <div class="section-box">
                <h6>Coke Unloading</h6>

                <div class="table-responsive">
                    <table class="table table-bordered text-center bg-white">
                        <thead>
                            <tr>
                                <th>Date</th>
                                <th>Shift</th>
                                <th>Bunker</th>
                                <th>A</th><th>B</th><th>C</th>
                                <th>D</th><th>E</th><th>F</th>
                                <th>Total</th>
                                <th>Position</th>
                                <th>Balance</th>
                            </tr>
                        </thead>

                        <tbody id="tblBody">
                            <!-- JS will generate rows -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Tonnage Sections -->
            <div class="row">

                <div class="col-md-6">
                    <div class="section-box">
                        <h6>Tonnage of Coke</h6>

                        <table class="table table-bordered bg-white text-center">
                            <thead>
                                <tr>
                                    <th>Bunker</th>
                                    <th>A</th><th>B</th><th>C</th>
                                    <th>D</th><th>E</th><th>F</th>
                                    <th>Total</th>
                                </tr>
                            </thead>
                            <tbody id="cokeTonnage"></tbody>
                        </table>
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="section-box">
                        <h6>Tonnage of Nut Coke</h6>

                        <table class="table table-bordered bg-white text-center">
                            <thead>
                                <tr>
                                    <th>Bunker</th>
                                    <th>A</th><th>B</th><th>C</th>
                                    <th>D</th><th>E</th><th>F</th>
                                    <th>Total</th>
                                </tr>
                            </thead>
                            <tbody id="nutTonnage"></tbody>
                        </table>
                    </div>
                </div>

            </div>
        </div>

        <!-- RIGHT SIDE -->
        <div class="col-md-4">

            <!-- Others -->
            <div class="section-box">
                <h6>Others</h6>

                <input class="form-control mb-2" placeholder="Eastern Bunker">
                <input class="form-control mb-2" placeholder="Western Bunker">
                <input class="form-control mb-2" placeholder="Middle Bunker">
            </div>

            <!-- Coke Received -->
            <div class="section-box">
                <h6>Coke Advised & Received</h6>

                <input class="form-control mb-2" placeholder="Material advised">
                <input class="form-control mb-2" placeholder="Time advised">
                <input class="form-control mb-2" placeholder="Material received">
                <input class="form-control mb-2" placeholder="Time received">
                <input class="form-control mb-2" placeholder="Unloaded">
                <input class="form-control mb-2" placeholder="Loco left">
                <input class="form-control mb-2" placeholder="Sent down">
                <input class="form-control mb-2" placeholder="Total">
            </div>

            <!-- Remarks -->
            <div class="section-box">
                <h6>Remarks & Delays</h6>
                <textarea class="form-control"></textarea>
            </div>

        </div>
    </div>

    <!-- FOOTER -->
    <div class="d-flex justify-content-end gap-2 mt-3">
        <button class="btn btn-success">Save</button>
        <button class="btn btn-danger">Delete</button>
        <button class="btn btn-secondary">Exit</button>
    </div>

</div>

<!-- JS for dynamic rows -->
<script>
    function generateRows(tableId, rows = 6) {
        let html = "";
        for (let i = 0; i < rows; i++) {
            html += "<tr>";
            for (let j = 0; j < 12; j++) {
                html += "<td><input type='text' class='form-control'></td>";
            }
            html += "</tr>";
        }
        document.getElementById(tableId).innerHTML = html;
    }

    generateRows("tblBody", 6);
    generateRows("cokeTonnage", 5);
    generateRows("nutTonnage", 5);
</script>

</body>
</html>