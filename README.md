<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light p-3">

<div class="container-fluid">
    <h4 class="mb-4">Cast House Details</h4>
    <div class="row mb-3">
        <div class="col-md-2">
            <label class="form-label">Date</label>
            <input type="date" class="form-control" value="2025-06-29">
        </div>
        <div class="col-md-2">
            <label class="form-label">Furnace</label>
            <input type="text" class="form-control" value="B">
        </div>
        <div class="col-md-2">
            <label class="form-label">Shift</label>
            <input type="text" class="form-control" value="B">
        </div>
    </div>

    <!-- Tap Hole Details -->
    <div class="card mb-3">
        <div class="card-header bg-primary text-white">Tap Hole Details</div>
        <div class="card-body table-responsive">
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th><th>Start</th><th>End</th><th>Gutko</th>
                        <th>Duration</th><th>Rate</th><th>TLC</th><th>OT</th>
                        <th>Clay</th><th>Condition</th><th>IMT Before</th><th>After</th>
                        <th>HM Temp</th><th>HM Weight</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>67108</td><td>13:40</td><td>15:45</td><td>125</td><td>2.0</td><td>4.48</td><td>2.6</td><td>DRY</td><td>DRY</td><td>NORMAL</td>
                        <td>1505</td><td>1500</td><td>1500</td><td>560.08</td>
                    </tr>
                    <tr>
                        <td>67109</td><td>16:00</td><td>18:15</td><td>130</td><td>2.25</td><td>5.00</td><td>3.0</td><td>DRY</td><td>DRY</td><td>NORMAL</td>
                        <td>1511</td><td>1516</td><td>1514</td><td>993.69</td>
                    </tr>
                    <tr>
                        <td>67110</td><td>18:15</td><td>20:20</td><td>175</td><td>2.08</td><td>3.85</td><td>3.5</td><td>DRY</td><td>DRY</td><td>NORMAL</td>
                        <td>1500</td><td>1500</td><td>1500</td><td>619.6</td>
                    </tr>
                    <tr>
                        <td>67111</td><td>19:50</td><td>22:35</td><td>165</td><td>2.0</td><td>3.85</td><td>2.8</td><td>DRY</td><td>DRY</td><td>NORMAL</td>
                        <td>1520</td><td>1525</td><td>1523</td><td>635.25</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Drilling Details -->
    <div class="card mb-3">
        <div class="card-header bg-secondary text-white">Drilling Details</div>
        <div class="card-body table-responsive">
            <table class="table table-bordered table-sm text-center">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th><th>Drill Dia</th><th>Drill Type</th><th>Bars</th>
                        <th>Lancing Pipe</th><th>Poking Rods</th><th>Air Pressure</th>
                        <th>Length</th><th>Hammering</th><th>Fumes</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>67108</td><td>57</td><td>DANGO</td><td>1</td><td>1</td><td></td><td></td><td>3.7</td><td></td><td></td></tr>
                    <tr><td>67109</td><td>57</td><td>DANGO</td><td>1</td><td>1</td><td></td><td></td><td>3.6</td><td></td><td></td></tr>
                    <tr><td>67110</td><td>57</td><td>DANGO</td><td>1</td><td>2</td><td></td><td></td><td>3.5</td><td></td><td></td></tr>
                    <tr><td>67111</td><td>55</td><td>DANGO</td><td>1</td><td></td><td></td><td></td><td>3.6</td><td></td><td></td></tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Mudgun Details -->
    <div class="card mb-3">
        <div class="card-header bg-info text-white">Mudgun Details</div>
        <div class="card-body table-responsive">
            <table class="table table-bordered table-sm text-center">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th><th>Closure Mode</th><th>Clay Qty</th><th>MG Clay Type</th>
                        <th>Mudgun Nozzle</th><th>Temp Before</th><th>Temp After</th>
                        <th>Initial Pressure</th><th>Max Pressure</th><th>Final Pressure</th><th>Clay Leakage</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>67108</td><td>MUDGUN</td><td>200</td><td>VISUVIUS</td><td>75</td><td>267</td><td>188</td><td>267</td><td>267</td><td>267</td><td>NO</td></tr>
                    <tr><td>67109</td><td>MUDGUN</td><td>192</td><td>VISUVIUS</td><td>65</td><td>268</td><td>224</td><td>268</td><td>268</td><td>268</td><td>NO</td></tr>
                    <tr><td>67110</td><td>MUDGUN</td><td>194</td><td>VISUVIUS</td><td>70</td><td>267</td><td>215</td><td>267</td><td>267</td><td>267</td><td>NO</td></tr>
                    <tr><td>67111</td><td>MUDGUN</td><td>190</td><td>VISUVIUS</td><td></td><td>268</td><td>221</td><td>268</td><td>268</td><td>268</td><td>NO</td></tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Buttons -->
    <div class="d-flex justify-content-between mt-4">
        <button class="btn btn-success">Save</button>
        <div>
            <button class="btn btn-primary">HM Logistics</button>
            <button class="btn btn-warning">Control/Pareto Chart</button>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>