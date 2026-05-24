  <div class="Main-Heading">
        Cast House Details
    </div> 
        <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
        <a id="tbFDatePick" class="btn btn-primary">
            <i class="fa fa-calendar"></i>
            <label id="currDate-value" style="font-size:12px;color:white"></label>
        </a>
        <input type="text" id="hiddenDate" style="position:absolute; opacity:0; height:0; width:0;" />
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
        <div>
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-12">
                        <div class="section-title">Tap Hole Details/Hot Metal Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:280px;">
                            <table class="table table-bordered table-sm text-center align-middle" id="TAP_Hot_Metal_Details">
                                <thead>
                                    <tr>
                                        <th class="Long_Heading freeze-col">Cast No</th>
                                        <th style="font-family:Georgia,serif;">Trough No</th>
                                        <th class="Long_Heading">Cast Start</th>
                                        <th class="Long_Heading">Cast End</th>
                                        <th class="Long_Heading">Gutko</th>
                                        <th class="Long_Heading_Medium">Cast Duration</th>
                                        <th style="max-width:70px;white-space:normal;word-wrap:break-word;font-family:Georgia,serif;">Casting Rate(t/min)</th>
                                        <th class="Long_Heading_Medium">TLC</th>
                                        <th class="Long_Heading_Medium">OT</th>
                                        <th class="Long_Heading_Medium">Cast Ready Time</th>
                                        <th style="max-width:90px;white-space:normal;word-wrap:break-word;font-family:Georgia,serif;">Splashing/Wetness Time</th>
                                        <th style="width:100px;min-width:100px;box-sizing:border-box;font-family:Georgia,serif;">Cast Type</th>
                                        <th style="width:110px;min-width:110px;box-sizing:border-box;font-family:Georgia,serif;">Clay Condition</th>
                                        <th style="width:160px;min-width:160px;box-sizing:border-box;font-family:Georgia,serif;">Taphole Behaviour at End Cast</th>
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
                </div>
            </div>
            <!-- Drilling Details -->
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-12">
                        <div class="section-Drill-title">Drilling Details/Slag Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:328px;">
                            <table class="table table-bordered text-center align-middle" id="Driling_Slag_Details">
                                <thead>
                                    <tr>
                                        <th class="Long_Heading freeze-col">Cast No</th>
                                        <th class="Long_Heading_Medium">Drill Dia</th>
                                        <th style="width:180px;min-width:180px;box-sizing:border-box;font-family:Georgia,serif;">Drill Type</th>
                                        <th class="Long_Heading_Medium">Total Drilling Time</th>
                                        <th class="Long_Heading_Medium">No of Drill Bars</th>
                                        <th class="Long_Heading_Medium">No of Drill Bits</th>
                                        <th class="Long_Heading_Medium">No of Lancing Pipe</th>
                                        <th class="Long_Heading_Medium">No of Poking Rods</th>
                                        <th class="Long_Heading_Medium">Drill Air Pressure</th>
                                        <th class="Long_Heading_Medium">TAP Hole Length</th>
                                        <th class="Long_Heading_Medium">Length Drilled Hammer</th>
                                        <th style="width:125px;min-width:125px;box-sizing:border-box;font-family:Georgia,serif;">Color of Furnes During Drilling</th>
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
                </div>
            </div>
            <!-- Mudgun Details -->
            <div class="form-section">
                <div class="section-title">Mudgun Details</div>
                <div class="table-responsive scrollable-table" style="max-height:300px;">
                    <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                        <thead>
                            <tr>
                                <th class="Long_Heading_Medium freeze-col">Cast No</th>
                                <th style="width:115px;min-width:115px;box-sizing:border-box;font-family:Georgia,serif;">Closure Mode</th>
                                <th style="width:70px;min-width:70px;box-sizing:border-box;font-family:Georgia,serif;">Clay Qty. Pushed</th>
                                <th style="width:180px;min-width:180px;box-sizing:border-box;font-family:Georgia,serif;">MG Clay Type</th>
                                <th class="Long_Heading_Medium">Lot No</th>
                                <th class="Long_Heading_Medium">No. of Bags</th>
                                <th class="Long_Heading_Medium">Mudgun Holding Time</th>
                                <th style="width:140px;min-width:140px;box-sizing:border-box;font-family:Georgia,serif;">Mudgun Nozzle</th>
                                <th class="Long_Heading_Medium">M.Nozzle Temp Before Closing</th>
                                <th class="Long_Heading_Medium">M.Nozzle Temp after Closing</th>
                                <th class="Long_Heading_Medium">Initial Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Max Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Final Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Pressure On Force</th>
                                <th style="width:90px;min-width:90px;box-sizing:border-box;font-family:Georgia,serif;">Clay Leakage</th>
                                <th style="width:90px;min-width:90px;box-sizing:border-box;font-family:Georgia,serif;">Back Fire</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
            <!--Other Details-->
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-4">
                        <div class="section-title">Other Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:280px;">
                            <table class="table table-bordered table-sm text-center align-middle" id="Other_Details">
                                <thead>
                                    <tr>
                                        <th class="Long_Heading_Medium freeze-col">Cast No</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;font-family:Georgia,serif;">Main Runner HM Amt</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;font-family:Georgia,serif;">Tilting Runner HM Amt</th>
                                        <th style="width:350px;min-width:350px;box-sizing:border-box;font-family:Georgia,serif;">Remarks</th>
                                    </tr>
                                </thead>
                                <tbody></tbody>
                            </table>
                        </div>
                    </div>
                    <div class="col-md-7">
                        <!-- Exception Cast Box -->
                        <fieldset class="border rounded p-3 shadow-sm mb-4">
                            <legend class="float-none w-auto px-2">
                                Exception Cast
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="SaveExceptionCast()">
                                    <b>Save</b>
                                </button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
                                <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
                                    <thead class="table-secondary sticky-top">
                                        <tr>
                                            <th class="idno" style="width:150px;">ID No</th>
                                            <th class="TapholeNo" style="width:50px;">TAPHOLE No</th>
                                            <th class="ExceptionDate" style="width:180px;">Date</th>
                                            <th class="hh" style="width:90px;">HH24</th>
                                            <th class="mm" style="width:90px;">MM</th>
                                            <th class="TapholeLength">Taphole Length</th>
                                            <th class="ClayPaused">Clay Paused</th>
                                            <th class="Type" style="width:240px;">Type</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <!-- rows created by JS -->
                                    </tbody>
                                </table>
                            </div>

                        </fieldset>
                        <!-- Carbon Paste Inj Box -->
                        <fieldset class="border rounded p-3 shadow-sm">
                            <legend class="float-none w-auto px-2">
                                Carbon Paste Inj
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">
                                    <b>Save</b>
                                </button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:255px;">
                                <table class="table table-bordered table-sm text-center align-middle" id="carbon_paste_inj">
                                    <thead>
                                        <tr>
                                            <th class="Heading_Small">Date Time</th>
                                            <th class="Heading_Small">Shift</th>
                                            <th class="Heading_Small">Below Tuyere</th>
                                            <th class="Heading_Small">No of Drum</th>
                                        </tr>
                                    </thead>

                                    <tbody></tbody>

                                </table>
                            </div>
                        </fieldset>
                    </div>
                    <div class="col-md-1">
                        <div>
                            <div>
                                <div class="mb-2">
                                    <button type="button" class="btnSaveCastHouse" onclick="SaveCastHouseData()">Save</button><br />
                                    <a id="lnkHML" class="btn btn-warning" style="width:90px;margin-left:28px;margin-top:5px;">HML</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <style>
        .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }
            .datepicker-days thead th.prev,
            .datepicker-days thead th.next {
                color: #000 !important;
            }


        .datepicker {
            z-index: 1055 !important;
        }
        /* ===== Headings ===== */
        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 10px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
            margin: 20px 0;
        }

        /* ===== Sections ===== */
        .form-section {
            background: #ffffff;
            padding: 10px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            border: 1px solid #ccc;
            font-family: Courier New, Courier, monospace;
        }

        .section-title,
        .section_Exception-title,
        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            font-weight: bold;
            border-radius: 10px;
            margin-bottom: 10px;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            font-size: 18px;
        }

        .section_Exception-title {
            font-size: 15px;
            width: 15vh;
        }

        .section-Drill-title {
            font-size: 20px;
            border-radius: 4px;
        }

        /* ===== Forms ===== */
        .form-control-lg {
            font-size: 1.5rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        .form-group {
            border-radius: 25px;
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        /* ===== Tables ===== */
        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
        }

        .table th,
        .table td {
            text-align: center;
            vertical-align: middle;
        }

        .scrollable-table {           
            overflow-y: auto;             
        }

        .table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
            border: 1px solid;
        }

        /* ===== Column Widths ===== */
        .Long_Heading {
            min-width: 80px;
            /*font-weight:bold;*/
            font-family:Georgia, serif;

        }

        .Long_Heading_Medium {
            min-width: 70px;
            /*font-weight:bold;*/
            font-family:Georgia, serif;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;            
            font-family:Georgia, serif;
        }

        .Heading_Small {
            width: 6px;
            white-space: nowrap;            
            font-family:Georgia, serif;
        }

        /* ===== Inputs ===== */
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
            font-weight:bold;
            font-family:Georgia, serif;
        }

        .highlight {
            background-color: #ffe08a !important;
        }

        /* ===== Buttons ===== */
        .btnSaveCastHouse {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 10px;
            color: #FFFFFF;
            cursor: pointer;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            font-weight: bold;
            line-height: 2.5;
            padding: 0 1rem;
            width: 12vh;
            margin-left: 30px;
            margin-top: 100px;
            transition: box-shadow .2s ease-in-out;
        }

            .btnSaveCastHouse:hover,
            .btnSaveCastHouse:focus {
                box-shadow: 0 0 .25rem rgba(0,0,0,.5), -.125rem -.125rem 1rem rgba(239,71,101,.5), .125rem .125rem 1rem rgba(255,154,90,.5);
            }

       

        /* ===== SweetAlert ===== */
        .my-swal-popup {
            font-family: Arial, sans-serif;
        }

        .my-swal-title {
            font-family: Georgia, serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: Verdana, sans-serif;
            font-size: 18px;
        }

        /* ===== Mudgun Clay Dropdown ===== */
        .mgClayWrapper {
            position: relative;
            display: flex;
            align-items: center;
        }

            .mgClayWrapper .mgClayInput {
                width: 100%;
            }

            .mgClayWrapper button {
                margin-left: 5px;
            }

        .mgClayList {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            z-index: 1000;
            top: 30px;
            left: 0;
            width: 200px;
            max-height: 200px;
            overflow-y: auto;
        }

            .mgClayList div {
                padding: 5px;
                cursor: pointer;
            }

                .mgClayList div:hover {
                    background: #eee;
                }

        /* ===== Misc ===== */
       
        fieldset {
            border: 2px solid #ccc !important;
            padding: 10px 12px 12px 12px;
        }

        legend {
            font-size: 24px;
            font-weight: 800;
            padding: 0 8px;
        }

        #Driling_Slag_Details tr.highlight td {
            background-color: yellow !important;
        }

        #TAP_Hot_Metal_Details tr.highlight td {
            background-color: yellow !important;
            
        }

        #Mudgun_Details tr.highlight td {
            background-color: yellow !important;
        }

        #Other_Details tr.highlight td {
            background-color: yellow !important;
        }
        /* ===== Tap Hole Freeze Column ===== */
        .freeze-col {
            position: sticky;
            left: 0;
            z-index: 3;
            background: #ffffff;
            border-right: 2px solid #666;
        }

        /* Header needs higher z-index */
        .table thead th.freeze-col {
            z-index: 5;
        }

        .modal-content {
            border-radius: 25px;
            border: none;
        }

        .modal-header {
            background: #0d6efd;
            color: #fff;
            border-radius: 25px 25px 0 0;
        }

        .title-box {
            background: #0d6efd;
            color: white;
            padding: 10px 25px;
            border-radius: 30px;
            text-align: center;
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 20px;
        }

        .clay-box {
            background: #0d6efd;
            border-radius: 25px;
            padding: 20px;
            color: white;
        }

        .clay-label {
            font-weight: 600;
        }

        .clay-input {
            border-radius: 10px;
        }

        .btn-save {
            background: #198754;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }

        .btn-exit {
            background: #dc3545;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }
    </style>
