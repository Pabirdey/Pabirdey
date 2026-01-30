@{
    ViewBag.Title = "Cast House Details";
    Layout = null;
}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">
    <style>
        /* ===== Headings ===== */
        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
            margin: 20px 0;
        }

        /* ===== Sections ===== */
        .form-section {
            background: #ffffff;
            padding: 20px;
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
            min-width: 130px;
        }

        .Long_Heading_Medium {
            min-width: 100px;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

        /* ===== Inputs ===== */
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
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

        .btnHMLogistics {
            margin: 10px;
            padding: 15px 30px;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            border: 0;
            background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
            background-size: 200% auto;
            cursor: pointer;
            transition: 0.5s;
            box-shadow: 0px 0px 14px -7px #f09819;
        }

            .btnHMLogistics:hover {
                background-position: right center;
            }

            .btnHMLogistics:active {
                transform: scale(0.95);
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
            width: 150px;
            max-height: 150px;
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
        #backgrcol_Tap_hole {           
            font-weight: bold;
            padding: 8px;
        }

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

</head>
<body>
    <div class="Main-Heading mt-3">Cast House Details</div>
    <div class="container-fluid mt-3">
        <div class="form-group">
            <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
            @*<input id="tbFDatePick" size="14" style="height:28px;text-align:center">*@
            <a id="tbFDatePick" class="drpickr btn btn-primary">
                <i class="fa fa-calendar"></i>
                <label id="currDate-value" style="font-size:12px;color:white"></label>
            </a>
            &nbsp;&nbsp;&nbsp;&nbsp;
            <span>
                <lable style="font-family:Allan,cursive;font-size:25px;">Furnace</lable>
                <select id="lstFur">
                    <option value="C">C</option>
                    <option value="D">D</option>
                    <option value="E">E</option>
                    <option value="F">F</option>
                    <option value="G">G</option>
                    <option value="H">H</option>
                    <option value="I">I</option>
                </select>
            </span>
        </div>
        <div class="mt-3">
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-12">
                        <div class="section-title">Tap Hole Details/Hot Metal Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:280px;">
                            <table class="table table-bordered table-sm text-center align-middle" id="TAP_Hot_Metal_Details">
                                <thead>
                                    <tr>
                                        <th class="Long_Heading_Medium freeze-col" id="backgrcol_Tap_hole">Cast No</th>
                                        <th id="backgrcol_Tap_hole">Trough No</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Cast Start</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Cast End</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Gutko</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Cast Duration</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Casting Rate(t/min)</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">TLC</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">OT</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Cast Ready Time</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole" style="max-width:90px;white-space:normal;word-wrap:break-word;">Splashing/Wetness Time</th>
                                        <th class="Long_Heading" style="width:132px;min-width:132px;box-sizing:border-box;">Cast Type</th>
                                        <th id="backgrcol_Tap_hole" style="width:132px;min-width:132px;box-sizing:border-box;">Clay Condition</th>
                                        <th id="backgrcol_Tap_hole" style="width:220px;min-width:220px;box-sizing:border-box;">Taphole Behaviour at End Cast</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">HMT Before Slag</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">HMT After Slag</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Final HM Temp</th>
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">HM Weight</th>
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
                                        <th class="Long_Heading_Medium freeze-col">Cast No</th>
                                        <th class="Long_Heading_Medium">Drill Dia</th>
                                        <th style="width:152px;min-width:152px;box-sizing:border-box;">Drill Type</th>
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
                                <th style="width:115px;min-width:115px;box-sizing:border-box;">Closure Mode</th>
                                <th style="width:115px;min-width:115px;box-sizing:border-box;">Clay Qty. Pushed</th>
                                <th style="width:195px;min-width:195px;box-sizing:border-box;">MG Clay Type</th>
                                <th class="Long_Heading_Medium">Lot No</th>
                                <th class="Long_Heading_Medium">No. of Bags</th>
                                <th class="Long_Heading_Medium">Mudgun Holding Time</th>
                                <th style="width:195px;min-width:150px;box-sizing:border-box;">Mudgun Nozzle</th>
                                <th class="Long_Heading_Medium">M.Nozzle Temp Before Closing</th>
                                <th class="Long_Heading_Medium">M.Nozzle Temp after Closing</th>
                                <th class="Long_Heading_Medium">Initial Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Max Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Final Plugin Pressure</th>
                                <th class="Long_Heading_Medium">Pressure On Force</th>
                                <th class="Long_Heading_Medium">Clay Leakage</th>
                                <th class="Long_Heading_Medium">Back Fire</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
            <!--Other Details-->
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-5">
                        <div class="section-title">Other Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:235px;">
                            <table class="table table-bordered table-sm text-center align-middle" id="Other_Details">
                                <thead>
                                    <tr>
                                        <th clas="freeze-col" style="width:100px;min-width:100px;box-sizing:border-box;">Cast No</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;">Main Runner HM Amt</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;">Tilting Runner HM Amt</th>
                                        <th style="width:350px;min-width:350px;box-sizing:border-box;">Remarks</th>
                                    </tr>
                                </thead>
                                <tbody></tbody>
                            </table>
                        </div>

                    </div>
                    <div class="col-md-5">
                        <!-- Exception Cast Box -->
                        <fieldset class="border rounded p-3 shadow-sm mb-4">
                            <legend class="float-none w-auto px-2">
                                Exception Cast
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveExceptionCast()">
                                    <b>Save</b>
                                </button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
                                <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
                                    <thead class="table-secondary sticky-top">
                                        <tr>
                                            <th style="width:150px;">ID No</th>
                                            <th style="width:180px;">Date</th>
                                            <th style="width:90px;">HH24</th>
                                            <th style="width:90px;">MM</th>
                                            <th>Taphole Length</th>
                                            <th>Clay Paused</th>
                                            <th style="width:240px;">Type</th>
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
                                <input type="hidden" id="saveUrl" value="@Url.Action("SaveCarbonPaste", "CastHouse")" />
                            </div>

                            <div class="table-responsive scrollable-table" style="max-height:255px;">
                                <table class="table table-bordered table-sm text-center align-middle"
                                       id="carbon_paste_inj">

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
                    <div class="col-md-2">
                        <div>
                            <div>
                                <div class="mb-2">
                                    <button type="button" class="btnSaveCastHouse" onclick="SaveCastHouseData()">Save</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Modal for Other MG Clay -->
    <div class="modal fade" id="mgClayOtherModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <!-- HEADER -->
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <!-- BODY -->
                <div class="modal-body">
                    <div class="title-box">Weightage of Clay</div>
                    <div class="clay-box">
                        <!-- Clay 1 (DROPDOWN) -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay1</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="clay1">
                                    <option value="">-- Select Clay1 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>
                        <!-- Clay 2 -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay2</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay2"> -->
                                <select class="form-select clay-input" id="clay2">
                                    <option value="">-- Select Clay2 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>
                        <!-- Clay 3 -->
                        <div class="row align-items-center">
                            <div class="col-2 clay-label">Clay3</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay3"> -->
                                <select class="form-select clay-input" id="clay3">
                                    <option value="">-- Select Clay3 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-save" onclick="saveData()">Save</button>
                    <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>
    <script src="~/bower_components/sweetalert/dist/Swwt2Alert.js"></script>
    <script>
        let lsSelectedFDate;
        let IsSelectedFur;
            $(document).ready(function() {
                //let today = new Date();
                //lsSelectedFDate = ("0" + today.getDate()).slice(-2) + "/" + ("0"+(today.getMonth()+1)).slice(-2) + "/" + today.getFullYear();
                var lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",new System.Globalization.CultureInfo("en-GB"))';
                $('#currDate-value').html(lsSelectedFDate);
                 $('#tbFDatePick').datepicker({
                     format: "dd/mm/yyyy",
                     autoclose: true,
                     todayHighlight: true
                 }).datepicker("setDate", lsSelectedFDate);

                IsSelectedFur = $('#lstFur').val();
                Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);                


    $('#lstFur').change(function(){
        IsSelectedFur = $(this).val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);       
    });

    $('#tbFDatePick').on('changeDate', function(){
        lsSelectedFDate = $('#date-daily1').datepicker('getFormattedDate');
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);        
    });
            });
          
           
            function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                        url: '/CastHouse/Get_TAP_Hole_Metal_Details',
                        type: 'GET',
                        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                        success: function (result_Tap_Hole_Metal) {
                            var parsedData = JSON.parse(result_Tap_Hole_Metal);
                            var tableBody = "";
                            for (var i = 0; i < parsedData.length; i++) {
                                tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
                                tableBody += `<td class="freeze-col"><input name="CAST_NO" class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                                tableBody += `<td><input name="TROUGH_NO" class='form-control form-control-sm' value='${parsedData[i].TROUGH_NO}' readonly/></td>`;
                                tableBody += `<td><input name="CAST_ST_TIME" class='form-control form-control-sm' value='${parsedData[i].CAST_ST_TIME}' readonly/></td>`;
                                tableBody += `<td><input name="CAST_END_TIME" class='form-control form-control-sm' value='${parsedData[i].CAST_END_TIME}' readonly/></td>`;
                                tableBody += `<td><input name="GUTKO" class='form-control form-control-sm' value='${parsedData[i].GUTKO}' readonly/></td>`;
                                tableBody += `<td><input name="CAST_DURATION" class='form-control form-control-sm' value='${parsedData[i].CAST_DURATION}' readonly/></td>`;
                                tableBody += `<td><input name="SPEED" class='form-control form-control-sm' value='${parsedData[i].SPEED}' readonly/></td>`;
                                tableBody += `<td><input name="NO_TLC" class='form-control form-control-sm' value='${parsedData[i].NO_TLC}' readonly/></td>`;
                                tableBody += `<td><input name="NO_OT" class='form-control form-control-sm' value='${parsedData[i].NO_OT}' readonly/></td>`;
                                tableBody += `<td><input name="CH_READY_TIME" class='form-control form-control-sm' value='${parsedData[i].CH_READY_TIME}'/></td>`;
                                tableBody += `<td><input name="SPLACING_WETNESS_TIME" class='form-control form-control-sm' value='${parsedData[i].SPLACING_WETNESS_TIME}'/></td>`;
                                tableBody += `<td>
                                <select name="CAST_TYPE" class ="form-select form-control-sm">
                                    <option value="" ${!parsedData[i].CAST_TYPE ? 'selected' : ''}></option>
                                    <option value="DRY" ${parsedData[i].CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option>
                                    <option value="NOT DRY" ${parsedData[i].CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
                                </select>
                              </td>`;
                                tableBody += `<td>
                                    <select name="CAST_CLAY_COND" class ="form-select form-control-sm">
                                        <option value="" ${!parsedData[i].CAST_CLAY_COND ? 'selected' : ''}></option>
                                        <option value="WET" ${parsedData[i].CAST_CLAY_COND === 'WET' ? 'selected' : ''}>WET</option>
                                        <option value="DRY" ${parsedData[i].CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
                                        <option value="EXCESS WET" ${parsedData[i].CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
                                        <option value="BLEEDING" ${parsedData[i].CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
                                    </select>
                                </td>`;
                            tableBody += `<td>
                                    <select name="TAPHOLE_BEHAVIOUR" class ="form-select form-control-sm">
                                        <option value="" ${!parsedData[i].TAPHOLE_BEHAVIOUR ? 'selected' : ''}></option>
                                        <option value="WIDE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected' : ''}>WIDE</option>
                                        <option value="NORMAL" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected' : ''}>NORMAL</option>
                                        <option value="WIDE+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option>
                                        <option value="NORMAL+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected' : ''}>NORMAL+COKE TROUBLE</option>
                                    </select>
                             </td>`;
                            tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control form-control-sm' value='${parsedData[i].HM_BEFORE_SLAG}'/></td>`;
                            tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control form-control-sm' value='${parsedData[i].HM_AFTER_SLAG}'/></td>`;
                            tableBody += `<td><input name="HM_TEMP" class='form-control form-control-sm' value='${parsedData[i].HM_TEMP}'/></td>`;
                            tableBody += `<td><input name="HM_WEIGHT" class='form-control form-control-sm' value='${parsedData[i].HM_WEIGHT}'/></td>`;
                            tableBody += `</tr>`;
                        }

                        $("#TAP_Hot_Metal_Details tbody").html(tableBody);
                    }
                });
            }
            
    </script>
</body>
</html>
