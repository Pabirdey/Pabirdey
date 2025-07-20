<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
        }
        .table-input {
            font-size: 0.85rem;
            padding: 2px 4px;
        }
        .form-section {
            background: #fff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        .section-title {
            background: #0d6efd;
            color: #fff;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
        }
        .form-control-sm {
            font-size: 0.75rem;
        }
    </style>
</head>
<body>
<div class="container-fluid mt-3">

    <div class="d-flex justify-content-between align-items-center mb-2">
        <h5>IITG System - Cast House Details</h5>
        <div>
            <label>Date: </label>
            <input type="date" class="form-control d-inline-block form-control-sm" style="width: 150px;" value="2025-07-20">
        </div>
    </div>

    <!-- Tap Hole Details -->
    <div class="form-section">
        <div class="section-title">Tap Hole Details</div>
        <div class="table-responsive">
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th>
                        <th>Start</th>
                        <th>End</th>
                        <th>Gutko</th>
                        <th>Duration</th>
                        <th>Casting Rate</th>
                        <th>TLC</th>
                        <th>Clay</th>
                        <th>Ready Time</th>
                        <th>Spl/Wet</th>
                        <th>Condition</th>
                        <th>Behaviour</th>
                        <th>HMT Before</th>
                        <th>HMT After</th>
                        <th>Final HM</th>
                        <th>Weight</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>67303</td>
                        <td>13:10</td>
                        <td>14:20</td>
                        <td>190.00</td>
                        <td>4.10</td>
                        <td>3.5</td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>DRY</td>
                        <td>NORMAL</td>
                        <td>1500</td>
                        <td>1500</td>
                        <td>1498</td>
                        <td>778.63</td>
                    </tr>
                    <tr>
                        <td>67304</td>
                        <td>13:50</td>
                        <td>15:00</td>
                        <td>120.00</td>
                        <td>5.62</td>
                        <td>2.3</td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>DRY</td>
                        <td>NORMAL</td>
                        <td>1489</td>
                        <td>1503</td>
                        <td>1506</td>
                        <td>673.95</td>
                    </tr>
                    <tr>
                        <td>67305</td>
                        <td>15:45</td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>DRY</td>
                        <td>NORMAL</td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Drilling Details -->
    <div class="form-section">
        <div class="section-title">Drilling Details</div>
        <table class="table table-bordered table-sm text-center align-middle">
            <thead class="table-light">
                <tr>
                    <th>Cast No</th>
                    <th>Drill Dia</th>
                    <th>Type</th>
                    <th>Total Bars</th>
                    <th>No of Bars</th>
                    <th>Lancing Pipe</th>
                    <th>Poking Rods</th>
                    <th>Air Pressure</th>
                    <th>Length</th>
                    <th>Hammer</th>
                </tr>
            </thead>
            <tbody>
                <tr><td>67303</td><td>65</td><td>DANGO</td><td>1</td><td>2</td><td></td><td></td><td></td><td>3.7</td><td></td></tr>
                <tr><td>67304</td><td>65</td><td>DANGO</td><td>1</td><td>2</td><td></td><td></td><td></td><td></td><td></td></tr>
                <tr><td>67305</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr>
            </tbody>
        </table>
    </div>

    <!-- Mudgun Details -->
    <div class="form-section">
        <div class="section-title">Mudgun Details</div>
        <table class="table table-bordered table-sm text-center align-middle">
            <thead class="table-light">
                <tr>
                    <th>Cast No</th>
                    <th>Mode</th>
                    <th>Clay Qty</th>
                    <th>MG Clay Type</th>
                    <th>Lot No</th>
                    <th>No. of Bags</th>
                    <th>Holding</th>
                    <th>Temp</th>
                    <th>Nozzle</th>
                    <th>Temp After Closing</th>
                    <th>Init Plug P</th>
                    <th>Max P</th>
                    <th>Final Force</th>
                    <th>Clay Leak</th>
                    <th>Back Fire</th>
                </tr>
            </thead>
            <tbody>
                <tr><td>67303</td><td>MUDGUN</td><td>197</td><td>VISUVIUS</td><td></td><td></td><td></td><td></td><td></td><td></td><td>233</td><td>270</td><td>NO</td><td>NO</td></tr>
                <tr><td>67304</td><td>MUDGUN</td><td>187</td><td>VISUVIUS</td><td></td><td></td><td></td><td></td><td></td><td></td><td>241</td><td>264</td><td>NO</td><td>NO</td></tr>
                <tr><td>67305</td><td>MUDGUN</td><td></td><td>VISUVIUS</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>NO</td><td>NO</td></tr>
            </tbody>
        </table>
    </div>

    <!-- Buttons -->
    <div class="d-flex gap-2 mb-5">
        <button class="btn btn-primary btn-sm">Save</button>
        <button class="btn btn-secondary btn-sm">HM Logistics</button>
        <button class="btn btn-info btn-sm">Control & Pareto Charts</button>
        <button class="btn btn-info btn-sm">Control and Pareto Chart</button>
    </div>

</div>
</body>
</html>