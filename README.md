<!DOCTYPE html>
<html>
<head>
    <title>Production Dashboard</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Icons -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons/font/bootstrap-icons.css" rel="stylesheet">

    <style>
        body {
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            min-height: 100vh;
        }

        .dashboard-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(12px);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.4);
            color: white;
        }

        .title {
            font-size: 26px;
            font-weight: 600;
            letter-spacing: 1px;
        }

        .table thead {
            background: linear-gradient(45deg, #f9d423, #ff4e50);
            color: white;
        }

        .table tbody tr {
            background-color: rgba(255,255,255,0.08);
            transition: 0.3s;
        }

        .table tbody tr:hover {
            background-color: rgba(255,255,255,0.15);
        }

        .form-control {
            border-radius: 10px;
            border: none;
        }

        .btn-modern {
            border-radius: 30px;
            padding: 8px 20px;
            font-weight: 500;
            transition: 0.3s;
        }

        .btn-modern:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .section-heading {
            font-weight: 600;
            margin: 25px 0 15px;
            font-size: 18px;
            letter-spacing: 1px;
            border-left: 4px solid #ffc107;
            padding-left: 10px;
        }
    </style>
</head>

<body>

<div class="container py-4">

    <div class="dashboard-card">

        <!-- Header -->
        <div class="d-flex justify-content-between align-items-center mb-4">
            <div class="title">
                <i class="bi bi-bar-chart-line-fill text-warning"></i> Production Dashboard
            </div>

            <div class="d-flex gap-3">
                <input type="date" class="form-control">
                <button class="btn btn-warning btn-modern">
                    <i class="bi bi-arrow-repeat"></i> Refresh
                </button>
            </div>
        </div>

        <!-- Production Table -->
        <div class="table-responsive">
            <table class="table table-bordered text-center align-middle text-white">
                <thead>
                    <tr>
                        <th>Date</th>
                        <th>Furnace</th>
                        <th>On Date</th>
                        <th>To Date</th>
                        <th>Plan On Date</th>
                        <th>Plan To Date</th>
                        <th>Balance</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>26-Feb-2026</td>
                        <td>C</td>
                        <td>2094.49</td>
                        <td>50700.21</td>
                        <td><input type="text" class="form-control text-center" value="2100"></td>
                        <td>50500</td>
                        <td class="fw-bold text-success">200.21</td>
                    </tr>

                    <tr>
                        <td>26-Feb-2026</td>
                        <td>E</td>
                        <td>1227.7</td>
                        <td>29949.52</td>
                        <td><input type="text" class="form-control text-center" value="1200"></td>
                        <td>30200</td>
                        <td class="fw-bold text-danger">-250.48</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Actual Breakup -->
        <div class="section-heading">ACTUAL BREAKUP</div>

        <div class="table-responsive">
            <table class="table table-bordered text-center align-middle text-white">
                <thead>
                    <tr>
                        <th></th>
                        <th>LD1</th>
                        <th>LD2</th>
                        <th>LD3</th>
                        <th>MRD TP</th>
                        <th>No of TP</th>
                        <th>Slag Ladle</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>On Date</td>
                        <td>6443.75</td>
                        <td>—</td>
                        <td>985.66</td>
                        <td>—</td>
                        <td><input type="text" class="form-control text-center" value="35.35"></td>
                        <td><input type="text" class="form-control text-center"></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Calculate Button -->
        <div class="text-end mt-3">
            <button class="btn btn-success btn-modern">
                <i class="bi bi-calculator"></i> Calculate Now
            </button>
        </div>

        <!-- Bottom Buttons -->
        <div class="d-flex justify-content-center gap-3 flex-wrap mt-4">
            <button class="btn btn-outline-light btn-modern">Save</button>
            <button class="btn btn-outline-light btn-modern">Back</button>
            <button class="btn btn-outline-light btn-modern">Raw Mat Cons</button>
            <button class="btn btn-outline-light btn-modern">Prod Details</button>
            <button class="btn btn-outline-light btn-modern">HM Distribution</button>
            <button class="btn btn-outline-light btn-modern">Delay Details</button>
        </div>

    </div>

</div>

</body>
</html>