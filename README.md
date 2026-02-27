<!DOCTYPE html>
<html>
<head>
    <title>Production</title>

    <!-- Bootstrap 5 CDN -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background-color: #0b2a4a;
        }

        .main-card {
            background: linear-gradient(to right, #2e7d32, #43a047);
            border-radius: 15px;
            padding: 20px;
            color: white;
        }

        .table thead {
            background-color: #f1c40f;
            color: black;
        }

        .table tbody td {
            background-color: #f9e79f;
        }

        .section-title {
            font-weight: bold;
            margin-top: 20px;
            margin-bottom: 10px;
        }

        .btn-custom {
            min-width: 120px;
        }
    </style>
</head>
<body>

<div class="container mt-4">
    <div class="main-card shadow-lg">

        <!-- Header -->
        <div class="d-flex justify-content-between align-items-center mb-3">
            <div>
                <label class="fw-bold">Date</label>
                <input type="date" class="form-control d-inline-block w-auto">
            </div>
            <button class="btn btn-light btn-custom">Refresh Balance</button>
        </div>

        <!-- Main Production Table -->
        <div class="table-responsive">
            <table class="table table-bordered text-center">
                <thead>
                    <tr>
                        <th>Date Time</th>
                        <th>Furnace</th>
                        <th>On Date</th>
                        <th>To Date</th>
                        <th>On Date</th>
                        <th>To Date</th>
                        <th>Balance</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>26-Feb-2026</td>
                        <td>C</td>
                        <td>2094.49</td>
                        <td>50700.21</td>
                        <td><input type="text" class="form-control" value="2100"></td>
                        <td>50500</td>
                        <td>200.21</td>
                    </tr>
                    <tr>
                        <td>26-Feb-2026</td>
                        <td>D</td>
                        <td colspan="5">--</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Actual Breakup Section -->
        <div class="section-title">ACTUAL BREAKUP</div>

        <div class="table-responsive">
            <table class="table table-bordered text-center">
                <thead>
                    <tr>
                        <th></th>
                        <th>LD1 Tons</th>
                        <th>LD2 Tons</th>
                        <th>LD3 Tons</th>
                        <th>MRD TP Tons</th>
                        <th>No of TP</th>
                        <th>No of Slag Ladle</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>On Date</td>
                        <td>6443.75</td>
                        <td></td>
                        <td>985.66</td>
                        <td></td>
                        <td><input type="text" class="form-control" value="35.35"></td>
                        <td><input type="text" class="form-control"></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Calculate Button -->
        <div class="text-end mb-3">
            <button class="btn btn-warning btn-custom">Calculate Now</button>
        </div>

        <!-- Bottom Buttons -->
        <div class="d-flex justify-content-center gap-3 flex-wrap">
            <button class="btn btn-light">Save</button>
            <button class="btn btn-light">Back</button>
            <button class="btn btn-light">Raw Mat Cons</button>
            <button class="btn btn-light">Prod Details</button>
            <button class="btn btn-light">HM Distribution</button>
            <button class="btn btn-light">Delay Details</button>
        </div>

    </div>
</div>

</body>
</html>