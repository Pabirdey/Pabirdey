@{
    Layout = null;   /* for testing – remove if using _Layout */
}
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>
    <!-- Bootstrap & jQuery -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <!-- Datepicker (load only once!) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>

    <style>
        /* Remove all borders while keeping layout */
        .table-bordered, .table-bordered th, .table-bordered td {
            border: none !important;
        }

        .input-wrapper {
            border: none !important;
        }

        .input-wrapper input {
            border: none !important;
        }

        fieldset {
            border: none !important;
        }

        .btnSaveCastHouse, .btnHMLogistics {
            border: none !important;
        }

        .list-box {
            border: 1px solid #999; /* keep dropdown list visible */
        }

        .table thead th {
            border: none !important; /* remove sticky header border */
        }

        /* Retain all your previous styles */
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
        }

        .my-swal-popup { font-family: 'Arial', sans-serif; }
        .my-swal-title { font-family: 'Georgia', serif; font-size: 22px; }
        .my-swal-text { font-family: 'Verdana', sans-serif; font-size: 18px; }

        .form-section {
            background: #ffffff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 18px;
        }

        .form-control-lg {
            font-size: 1.5rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        .scrollable-table {
            overflow-y: auto;
        }

        .Long_Heading_Medium { min-width: 100px; }
        .Long_Heading { min-width: 130px; }
        .Heading_Small { width: 10px; white-space: nowrap; }
        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 20px;
        }

        .form-group {
            border-radius: 25px;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        select { appearance: auto !important; -webkit-appearance: auto !important; -moz-appearance: auto !important; }

        .Main-Heading {
            font-family: Allan,cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
        }

        .input-wrapper {
            display: flex;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box div {
            padding: 5px;
            cursor: pointer;
        }

        .list-box div:hover { background: #e6e6e6; }
    </style>
</head>
<body>
    <div class="Main-Heading mt-0">Cast House Details</div>
    <div class="container-fluid mt-0">
        <div class="form-group">
            <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
            <input id="tbFDatePick" size="14" style="height:28px;text-align:center">
            &nbsp;&nbsp;&nbsp;&nbsp;
            <span>
                <lable style="font-family:Allan,cursive;font-size:25px;">Furnace</lable>
                <select id="lstFur">
                    <option value="C">C</option>
                    <option value="E">E</option>
                    <option value="F">F</option>
                    <option value="G">G</option>
                    <option value="H">H</option>
                    <option value="I">I</option>
                </select>
            </span>
        </div>

        <!-- Tables: Tap Hole, Drilling, Mudgun, Other Details -->
        <!-- Keep your existing HTML structure exactly the same -->
        <div class="mt-1">
            <!-- Tap Hole Table -->
            <div class="form-section">
                <div class="section-title">Tap Hole Details/Hot Metal Details</div>
                <div class="table-responsive scrollable-table" style="max-height:300px;">
                    <table class="table table-bordered table-sm text-center align-middle" id="TAP_Hot_Metal_Details">
                        <thead>
                            <tr>
                                <th class="Long_Heading_Medium">Cast No</th>
                                <th>Trough No</th>
                                <th class="Long_Heading_Medium">Cast Start</th>
                                <th class="Long_Heading_Medium">Cast End</th>
                                <th class="Long_Heading_Medium">Gutko</th>
                                <th class="Long_Heading_Medium">Cast Duration</th>
                                <th class="Long_Heading_Medium">Casting Rate(t/min)</th>
                                <th class="Long_Heading_Medium">TLC</th>
                                <th class="Long_Heading_Medium">OT</th>
                                <th class="Long_Heading_Medium">Cast Ready Time</th>
                                <th class="Long_Heading_Medium" style="max-width:90px;white-space:normal;word-wrap:break-word;">Splashing/Wetness Time</th>
                                <th class="Long_Heading" style="width:132px;min-width:132px;">Cast Type</th>
                                <th style="width:132px;min-width:132px;">Clay Condition</th>
                                <th style="width:220px;min-width:220px;">Taphole Behaviour at End Cast</th>
                                <th class="Long_Heading_Medium">HMT Before Slag</th>
                                <th class="Long_Heading_Medium">HMT After Slag</th>
                                <th class="Long_Heading_Medium">Final HM Temp</th>
                                <th class="Long_Heading_Medium">HM Weight</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- Drilling Table -->
            <div class="form-section">
                <div class="section-Drill-title">Drilling Details/Slag Details</div>
                <div class="table-responsive scrollable-table" style="max-height:320px;">
                    <table class="table table-bordered text-center align-middle" id="Driling_Slag_Details">
                        <thead>
                            <tr>
                                <th class="Long_Heading_Medium">Cast No</th>
                                <th class="Long_Heading_Medium">Drill Dia</th>
                                <th style="width:152px;min-width:152px;">Drill Type</th>
                                <th class="Long_Heading_Medium">Total Drilling Time</th>
                                <th class="Long_Heading_Medium">No of Drill Bars</th>
                                <th class="Long_Heading_Medium">No of Drill Bits</th>
                                <th class="Long_Heading_Medium">No of Lancing Pipe</th>
                                <th class="Long_Heading_Medium">No of Poking Rods</th>
                                <th class="Long_Heading_Medium">Drill Air Pressure</th>
                                <th class="Long_Heading_Medium">TAP Hole Length</th>
                                <th class="Long_Heading_Medium">Length Drilled Hammer</th>
                                <th class="Long_Heading_Medium">Color of Furnes During Drilling</th>
                                <th class="Long_Heading_Medium">Slag Start Time</th>
                                <th class="Long_Heading_Medium">Slag Time Ratio</th>
                                <th class="Long_Heading_Medium">Slag Retention Time</th>
                                <th class="Long_Heading_Medium">No of Slag Ladle</th>
                                <th class="Long_Heading_Medium">No of Cinder Granulation</th>
                                <th class="Long_Heading_Medium">Granulation Perc</th>
                                <th class="Long_Heading_Medium">Cinder Theoretical Wt</th>
                                <th class="Long_Heading_Medium">Slag Rate</th>
                                <th class="Long_Heading_Medium">Total Slag</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- Mudgun Table -->
            <div class="form-section">
                <div class="section-title">Mudgun Details</div>
                <div class="table-responsive scrollable-table" style="max-height:318px;">
                    <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                        <thead>
                            <tr>
                                <th class="Long_Heading_Medium">Cast No</th>
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
                                <th>Pressure On Force</th>
                                <th>Clay Leakage</th>
                                <th>Back Fire</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- ================= MODAL ================= -->
    <div class="modal fade" id="clayModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title w-100 text-center">MG CLAY DETAILS</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label>Clay 1</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label>Clay 2</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label>Clay 3</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-success" data-bs-dismiss="modal">Save</button>
                    <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
