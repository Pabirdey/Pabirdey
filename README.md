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
            max-height: 270px; 
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
            <h2>Cast House Details</h2>            
        </div>       
        <!-- Tap Hole Details -->
        <div>
            <label>Date:</label>
            <span><input type="date" /></span>
            <lable>Furnace</lable>
            <select>
                <option value="C">C</option>
                <option value="D">D</option>
                <option value="E">E</option>
                <option value="F">F</option>
                <option value="G">G</option>
                <option value="H">H</option>
                <option value="I">I</option>
            </select>
        </div>
        <div class="form-section">
            <div class="section-title">Tap Hole Details</div>
            <div class="table-responsive">
                <table class="table table-bordered table-sm text-center align-middle">
                    <thead class="table-light">
                        <tr>
                            <th>Cast No</th>
                            <th>Trough No</th>
                            <th>Cast Start</th>
                            <th>Cast End</th>
                            <th>Gutko</th>
                            <th>Cast Duration</th>
                            <th>Casting Rate(t/min)</th>
                            <th>TLC</th>
                            <th>OT</th>
                            <th>Cast Ready Time</th>
                            <th>Splashing/Wetness Time</th>
                            <th>Cast Type</th>
                            <th>Clay Condition</th>
                            <th>Taphole Behaviour at End Cast</th>                            
                        </tr>
                    </thead>                  
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
                        <th>Drill Type</th>
                        <th>Total Drilling Time</th>
                        <th>No of Drill Bars</th>
                        <th>No of Drill Bits</th>
                        <th>No of Lancing Pipe</th>
                        <th>No of Poking Rods</th>
                        <th>Drill Air Pressure</th>
                        <th>TAP Hole Length</th>
                        <th>Length Drilled Hammer</th>
                        <th>Color of Furnes During Drilling</th>
                    </tr>
                </thead>                
            </table>
        </div>
        <!-- Mudgun Details -->
        <div class="form-section">
            <div class="section-title">Mudgun Details</div>
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th>
                        <th>Closure Mode</th>
                        <th>Clay Qty. Pushed</th>
                        <th>MG Clay Type</th>
                        <th>Lot No</th>
                        <th>No. of Bags</th>
                        <th>Mudgun Holding Time</th>
                        <th>Mudgun Nozzle</th>
                        <th>M.Nozzle Temp Before Closing</th>
                        <th>M.Nozzle Temp after Closing</th>
                        <th>Initial Plugin Pressure</th>
                        <th>Max Plugin Pressure</th>
                        <th>Final Plugin Pressure</th>
                        <th>Clay Leak</th>
                        <th>Back Fire</th>
                    </tr>
                </thead>                
            </table>
        </div>
        <!--Other Details-->
        <div class="form-section">
            <div class="section-title">Other Details</div>
            <table class="table table-bordered table-sm text-center align-middle">
                <thead class="table-light">
                    <tr>
                        <th>Cast No</th>
                        <th>Main Runner HM Amt</th>
                        <th>Tilting Runner HM Amt</th>
                        <th>Remarks</th>
                    </tr>
                </thead>
            </table>
        </div>
        <!-- Buttons -->       
    </div>
</body>
</html>
