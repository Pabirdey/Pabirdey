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
            background: #8053A8;
            color: #fff;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
            text-align:center;
        }

        .form-control-sm {
            font-size: 0.75rem;            
        }
        th{
            font-family:Courier New, Courier, monospace;
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
            <span><input type="date" id="tbToDatePick"/></span>
            <lable>Furnace</lable>
            <select id="lstFur">
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
            <div class="row g-0">                
                <div class="col-md-8">
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
                            <tbody>                                
                            </tbody>
                        </table>
                    </div>
                </div>                
                <div class="col-md-4">
                    <div class="section-title">Hot Metal Details</div>
                    <div class="table-responsive">
                        <table class="table table-bordered table-sm text-center align-middle">
                            <thead class="table-light">
                                <tr>
                                    <th class="Long_Heading">HMT Before Slag</th>
                                    <th class="Long_Heading">HMT After Slag</th>
                                    <th class="Long_Heading">Final HM Temp</th>
                                    <th class="Long_Heading">HM Weight</th>
                                </tr>
                            </thead>
                            <tbody>                               
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
        <!-- Drilling Details -->
        <div class="form-section">
            <div class="row g-0">
                <div class="col-md-6">
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
                        <tbody id="CastDetailsBody"></tbody>
                    </table>
                </div>
                <div class="col-md-6">
                    <div class="section-title">Slag Details</div>
                    <div class="table-responsive">
                        <table class="table table-bordered table-sm text-center align-middle">
                            <thead class="table-light">
                                <tr>
                                    <th>Slag Start Time</th>
                                    <th>Slag Time Ratio</th>
                                    <th>Slag Retention Time</th>
                                    <th>No of Slag Ladle</th>
                                    <th>No of Cinder Granulation</th>
                                    <th>Granulation Perc</th>
                                    <th>Cinder Theoretical Wt</th>
                                    <th>Slag Rate</th>
                                    <th>Total Slag</th>
                                </tr>
                            </thead>
                            <tbody></tbody>
                        </table>
                    </div>
                </div>
            </div>
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
                <tbody id="CastDetailsBody"></tbody>              
            </table>
        </div>
        <!--Other Details-->
        <div class="form-section">
            <div class="row g-0">
                <div class="col-md-4">
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
                        <tbody id="CastDetailsBody"></tbody>
                    </table>
                </div>
                <div class="col-md-4">
                    <div class="section-title">Exception Cast</div>
                    <table class="table table-bordered table-sm text-center align-middle">
                        <thead class="table-light">
                            <tr>
                                <th>ID No</th>
                                <th>Taphole No</th>
                                <th>Date Time</th>
                                <th>HH24</th>
                                <th>MM</th>
                                <th>Taphole Length</th>
                                <th>Clay Pushed</th>
                                <th>Type</th>
                            </tr>
                        </thead>
                        <tbody id="CastDetailsBody"></tbody>
                    </table>
                    <div>
                        <!--Carbon Paste Inj-->
                        <div class="section-title">Carbon Paste Inj</div>
                        <table class="table table-bordered table-sm text-center align-middle">
                            <thead class="table-light">
                                <tr>
                                    <th>Date Time</th>
                                    <th>Shift</th>
                                    <th>Below Tuyere</th>
                                    <th>No Of Drum</th>
                                </tr>
                            </thead>
                            <tbody id="CastDetailsBody"></tbody>
                        </table>
                    </div>       
                </div>

                <div class="col-md-2">                    
                    <button type="button" class="btn btn-primary">Save</button>
                    <button type="button" class="btn btn-warning">HM Logistics</button>
                </div>
            </div>
        </div>
       
    </div>
</body>
</html>

