<!DOCTYPE html>
<html>
<head>
    <title>Production Dashboard</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons/font/bootstrap-icons.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container py-4">

    <div class="card shadow-lg rounded-4">

        <div class="card-body">

            <!-- Header -->
            <div class="d-flex justify-content-between align-items-center mb-4">
                <h4 class="fw-bold mb-0">
                    <i class="bi bi-bar-chart"></i> Production
                </h4>

                <div class="d-flex gap-2">
                    <input type="date" class="form-control">
                    <button class="btn btn-primary">
                        <i class="bi bi-arrow-repeat"></i> Refresh
                    </button>
                </div>
            </div>

            <!-- Production Table -->
            <div class="table-responsive">
                <table class="table table-bordered table-hover text-center align-middle">
                    <thead class="table-dark">
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
                            <td>
                                <input type="text" class="form-control text-center" value="2100">
                            </td>
                            <td>50500</td>
                            <td class="fw-bold text-success">200.21</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>E</td>
                            <td>1227.7</td>
                            <td>29949.52</td>
                            <td>
                                <input type="text" class="form-control text-center" value="1200">
                            </td>
                            <td>30200</td>
                            <td class="fw-bold text-danger">-250.48</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Actual Breakup -->
            <h5 class="mt-4 mb-3 fw-semibold border-bottom pb-2">
                ACTUAL BREAKUP
            </h5>

            <div class="table-responsive">
                <table class="table table-bordered table-hover text-center align-middle">
                    <thead class="table-secondary">
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
                            <td class="fw-semibold">On Date</td>
                            <td>6443.75</td>
                            <td>-</td>
                            <td>985.66</td>
                            <td>-</td>
                            <td>
                                <input type="text" class="form-control text-center" value="35.35">
                            </td>
                            <td>
                                <input type="text" class="form-control text-center">
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Calculate Button -->
            <div class="text-end mt-3">
                <button class="btn btn-success">
                    <i class="bi bi-calculator"></i> Calculate Now
                </button>
            </div>

            <!-- Bottom Buttons -->
            <div class="d-flex justify-content-center gap-3 flex-wrap mt-4">
                <button class="btn btn-outline-primary">Save</button>
                <button class="btn btn-outline-secondary">Back</button>
                <button class="btn btn-outline-info">Raw Mat Cons</button>
                <button class="btn btn-outline-warning">Prod Details</button>
                <button class="btn btn-outline-dark">HM Distribution</button>
                <button class="btn btn-outline-danger">Delay Details</button>
            </div>

        </div>
    </div>

</div>

</body>
</html>