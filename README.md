<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #eef2f7;
        }

        .header {
            background: #0d47a1;
            color: white;
            padding: 12px;
            border-radius: 10px;
            font-weight: bold;
            font-size: 20px;
        }

        .section-box {
            background: linear-gradient(to right, #1565c0, #1e88e5);
            color: white;
            border-radius: 15px;
            padding: 15px;
            margin-bottom: 15px;
        }

        .section-title {
            font-weight: bold;
            margin-bottom: 10px;
        }

        .form-control, .form-select {
            height: 30px;
            padding: 2px 6px;
            font-size: 12px;
        }

        table th, table td {
            font-size: 12px;
            padding: 4px;
        }

        .btn-custom {
            width: 100px;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">

    <!-- HEADER -->
    <div class="header">
        FURNACE HIGH LINE LOG SHEET
    </div>

    <!-- TOP BAR -->
    <div class="row mt-2 mb-3">
        <div class="col-md-3">
            <label>Timestamp</label>
            <input type="date" class="form-control">
        </div>

        <div class="col-md-3">
            <label>Shift</label>
            <select class="form-select">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </div>
    </div>

    <div class="row">

        <!-- LEFT PANEL -->
        <div class="col-md-5">
            <div class="section-box">
                <div class="section-title">High Line Log</div>

                <table class="table table-bordered text-center bg-white text-dark">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Recd.</th>
                            <th>Retd.</th>
                            <th>Reason</th>
                            <th>U/L</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>LRP (FLB)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>JODA</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>PELLET</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>

                <div class="text-end">
                    <strong>Total: 35 / 7</strong>
                </div>
            </div>

            <!-- Remarks -->
            <div class="section-box">
                <div class="section-title">Remarks & Delays</div>
                <textarea class="form-control" rows="3"></textarea>
            </div>
        </div>

        <!-- CENTER PANEL -->
        <div class="col-md-4">
            <div class="section-box">
                <div class="section-title">Furnaces</div>

                <table class="table table-bordered text-center bg-white text-dark">
                    <thead>
                        <tr>
                            <th></th>
                            <th>DMAG</th>
                            <th>KO</th>
                            <th>BELT</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>SP1</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SP2</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- TOTAL -->
            <div class="section-box">
                <div class="section-title">Total</div>

                <table class="table table-bordered text-center bg-white text-dark">
                    <tr>
                        <th>SP1</th>
                        <td>0</td>
                        <td>8</td>
                        <td>1350</td>
                        <td>1670</td>
                    </tr>
                    <tr>
                        <th>SP2</th>
                        <td>0</td>
                        <td>0</td>
                        <td>0</td>
                        <td>0</td>
                    </tr>
                </table>
            </div>
        </div>

        <!-- RIGHT PANEL -->
        <div class="col-md-3">

            <div class="section-box">
                <div class="section-title">Sinter Storage</div>

                <label>SP1</label>
                <input class="form-control mb-2">

                <label>SP2</label>
                <input class="form-control mb-2">

                <label>Total Fines</label>
                <input class="form-control">
            </div>

            <div class="section-box">
                <div class="section-title">Reclaimed Ore</div>

                <label>LRP</label>
                <input class="form-control mb-2">

                <label>Direct Fines</label>
                <input class="form-control mb-2">

                <label>Reclaimed Fines</label>
                <input class="form-control">
            </div>

            <div class="section-box">
                <div class="section-title">FLB Data</div>

                <table class="table table-bordered bg-white text-dark">
                    <tr>
                        <th>Material</th>
                        <th>Position</th>
                    </tr>
                    <tr>
                        <td>
                            <select class="form-select">
                                <option>PYROXINITE</option>
                                <option>LRP</option>
                            </select>
                        </td>
                        <td><input class="form-control"></td>
                    </tr>
                </table>
            </div>

            <!-- BUTTONS -->
            <div class="text-center mt-3">
                <button class="btn btn-success btn-custom">Save</button>
                <button class="btn btn-danger btn-custom">Delete</button>
                <button class="btn btn-secondary btn-custom">Exit</button>
            </div>

        </div>

    </div>

</div>

</body>
</html>