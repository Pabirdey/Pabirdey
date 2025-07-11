<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        th.long-header{
            white-space:normal;  
            word-wrap: break-word;              
            max-width: 70px;           
            
        }
        th{
            font-size:12px;
        }
    </style>

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
            <input type="text" class="form-control" value="I">
        </div>        
    </div>

    <!-- Tap Hole Details -->
    <div class="card mb-4">
        <div class="card-header bg-primary text-white">Tap Hole Details</div>
        <div class="card-body table-responsive">
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th><th>Trough</th><th>Cast Start</th><th>Cast End</th>
                        <th>Gutko</th><th class="long-header">Cast Duration</th><th class="long-header">Casting Rate(t/min)</th><th>TLC</th>
                        <th>OT</th><th class="long-header">Cast Ready Time</th><th class="long-header">Splashing Wetness Time</th>
                        <th class="long-header">Cast Type</th><th class="long-header">Clay Condition</th><th class="long-header">Taphole Behaviour at End Cast</th>
                    </tr>
                </thead>
                <tbody>                    
                </tbody>
            </table>
        </div>
        <div class="card mb-3">
            <div class="card-header bg-secondary text-white">Hot Metal Details</div>
            <div class="card-body table-responsive">
                <table class="table table-bordered table-sm text-center">
                    <thead class="table-light">
                        <tr>
                            <th class="long-header">HMT Before Slag</th><th class="long-header">HMT After Slag</th>
                            <th>Final HM Temp</th><th>HM Weight</th>                            
                        </tr>
                    </thead>
                    <tbody>                    
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Drilling Details -->
     

    <!-- Mudgun Details -->
    <!-- <div class="card mb-3">
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
                </tbody>
            </table>
        </div>
    </div>

     Buttons -->
    <!-- <div class="d-flex justify-content-between mt-4">
        <button class="btn btn-success">Save</button>
        <div>
            <button class="btn btn-primary">HM Logistics</button>
            <button class="btn btn-warning">Control/Pareto Chart</button>
        </div>
    </div> --> 
</div> 

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
