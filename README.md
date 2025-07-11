<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .table-sm td, .table-sm th {
            padding: 0.25rem;
            font-size: 13px;
        }
        .highlight-yellow { background-color: yellow; }
        .highlight-blue { background-color: #cce5ff; }
        .section-title {
            background-color: #f8f9fa;
            padding: 8px;
            font-weight: bold;
            border: 1px solid #dee2e6;
        }
    </style>
</head>
<body class="p-3">
    <div class="container-fluid">

        <h4 class="mb-4">Cast House Details</h4>

        <!-- Header Section -->
        <div class="row mb-3">
            <div class="col-md-2">
                <label class="form-label fw-bold">Furnace</label>
                <input type="text" class="form-control form-control-sm">
            </div>
            <div class="col-md-2">
                <label class="form-label fw-bold">MWL/FUR Name</label>
                <input type="text" class="form-control form-control-sm">
            </div>
            <div class="col-md-2">
                <label class="form-label fw-bold">Shift</label>
                <input type="text" class="form-control form-control-sm">
            </div>
            <div class="col-md-2">
                <label class="form-label fw-bold">Date</label>
                <input type="date" class="form-control form-control-sm">
            </div>
        </div>

        <!-- Top Table Section -->
        <div class="section-title">Top Hole Details + Hot Metal Details</div>
        <div class="table-responsive mb-4">
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th class="highlight-yellow">Cast</th>
                        <th>No</th>
                        <th>Start</th>
                        <th>End</th>
                        <th>Duration</th>
                        <th>Clay</th>
                        <th>Ready Time</th>
                        <th>Tap Hole</th>
                        <th>HMT Before</th>
                        <th>HMT After</th>
                        <th>Final Wt</th>
                        <th>HM Weight</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="highlight-yellow">CAST-1</td>
                        <td>10</td>
                        <td>10:00</td>
                        <td>10:30</td>
                        <td>30m</td>
                        <td>GOOD</td>
                        <td>10:45</td>
                        <td>TAPHOLE-A</td>
                        <td class="highlight-blue">BEFORE</td>
                        <td class="highlight-blue">AFTER</td>
                        <td class="highlight-blue">5.6T</td>
                        <td class="highlight-blue">HM12345</td>
                    </tr>
                    <!-- Repeat rows as needed -->
                </tbody>
            </table>
        </div>

        <!-- Bottom Table Section -->
        <div class="section-title">Slag & Drill Details</div>
        <div class="table-responsive">
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th class="highlight-yellow">Cast</th>
                        <th>Drill ID</th>
                        <th>Initial Drill</th>
                        <th>Slag Start</th>
                        <th>Slag Time</th>
                        <th>Retention</th>
                        <th>Granulation</th>
                        <th>Cinder</th>
                        <th>Slag Rate</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="highlight-yellow">CAST-2</td>
                        <td>DRILL-01</td>
                        <td>10:00</td>
                        <td>10:05</td>
                        <td>5min</td>
                        <td>RETENTION</td>
                        <td class="highlight-blue">ENABLED</td>
                        <td class="highlight-blue">YES</td>
                        <td class="highlight-blue">1.23 T/min</td>
                    </tr>
                    <!-- Repeat rows -->
                </tbody>
            </table>
        </div>

    </div>
</body>
</html>