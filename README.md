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

    </style>

</head>
<body>
    <div class="Main-Heading mt-3">Cast House Details</div>
    <div class="container-fluid mt-3">
        <div class="form-group">
            <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
            <input id="tbFDatePick" size="14" style="height:28px;text-align:center">
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
                                        <th class="Long_Heading_Medium" id="backgrcol_Tap_hole">Cast No</th>
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
                                        <th class="Long_Heading_Medium">Cast No</th>
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
                                <th class="Long_Heading_Medium">Cast No</th>
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
                                        <th style="width:100px;min-width:100px;box-sizing:border-box;">Cast No</th>
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
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Other MG Clay Type</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <input type="hidden" id="hdnRowIndex">
                    <input type="text" id="txtOtherMGClay" class="form-control" placeholder="Enter MG Clay Type">
                </div>
                <div class="modal-footer">
                    <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                    <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
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
                let today = new Date();
                lsSelectedFDate = ("0" + today.getDate()).slice(-2) + "/" + ("0"+(today.getMonth()+1)).slice(-2) + "/" + today.getFullYear();
                 $('#tbFDatePick').datepicker({
                     format: "dd/mm/yyyy",
                     autoclose: true,
                     todayHighlight: true
                   }).val(lsSelectedFDate);

                IsSelectedFur = $('#lstFur').val();
                Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
                Display_Driling_Details(lsSelectedFDate, IsSelectedFur);
                Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
                Display_Other_Details(lsSelectedFDate, IsSelectedFur);
                Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur);


    $('#lstFur').change(function(){
        IsSelectedFur = $(this).val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        Display_Driling_Details(lsSelectedFDate, IsSelectedFur);
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        Display_Other_Details(lsSelectedFDate, IsSelectedFur);
        Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur);
    });

    $('#tbFDatePick').on('changeDate', function(){
        lsSelectedFDate = $(this).val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        Display_Driling_Details(lsSelectedFDate, IsSelectedFur);
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        Display_Other_Details(lsSelectedFDate, IsSelectedFur);
        Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur);
    });
            });
            function getShiftFromTime(dt) {
                if (!dt) return "A";
                var date = new Date(dt);
                var hour = date.getHours();
                var min = date.getMinutes();
                var totalMin = hour * 60 + min;
                if (totalMin >= 360 && totalMin < 840) {
                    return "A";
                }
                if (totalMin >= 840 && totalMin < 1320) {
                    return "B";
                }
                return "C";
            }
            /*********************Row Highlight Yellow Color For Same Cast No*******************************/
            $(document).on("click", "#Driling_Slag_Details *, #TAP_Hot_Metal_Details *,#Mudgun_Details *,#Other_Details *", function () {
                debugger;
                let row = $(this).closest("tr");
                if (!row.length) return;
                let castNo = row.attr("data-castno");
                if (!castNo) return;
                castNo = castNo.trim();
                $("#Driling_Slag_Details tr").removeClass("highlight");
                $("#TAP_Hot_Metal_Details tr").removeClass("highlight");
                $("#Mudgun_Details tr").removeClass("highlight");
                $("#Other_Details tr").removeClass("highlight");

                $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
                $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
                $('#Mudgun_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
                $('#Other_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
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
                                tableBody += `<td><input name="CAST_NO" class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
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
            function Display_Mudgun_Details(date, furnace){
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
                    type: 'GET',
                    data: { Fdate: date, Fur: furnace },
                    success: function(result){
                        let parsedData = JSON.parse(result);
                        let tableBody = "";
                        for(let i=0;i<parsedData.length;i++){
                            tableBody += "<tr>";
                            tableBody += `<td>${parsedData[i].CAST_NO}</td>`;
                            tableBody += `<td>
                                            <select class="form-select form-select-sm">
                                                <option value="" ${parsedData[i].CLOSURE_MODE==""?'selected':''}></option>
                                                <option value="MUDGUN" ${parsedData[i].CLOSURE_MODE=="MUDGUN"?'selected':''}>MUDGUN</option>
                                                <option value="NULL" ${parsedData[i].CLOSURE_MODE=="NULL"?'selected':''}>NULL</option>
                                            </select>
                                          </td>`;
                            tableBody += `<td><input class="form-control form-control-sm" value="${parsedData[i].CLAY_QUANTITY}"></td>`;
                            // Editable MG Clay input + dropdown + modal
                            tableBody += `<td>
                                            <div class="mgClayWrapper">
                                                <input type="text" class ="form-control form-control-sm mgClayInput" value="${parsedData[i].MG_CLAY_USED}">
                                                <button type="button" class="btn btn-sm btn-secondary" onclick="showDropdown(this)">▼</button>
                                                <div class="mgClayList">
                                                    <div onclick="selectClay(this, ${i})">ACE</div>
                                                    <div onclick="selectClay(this, ${i})">BRL</div>
                                                    <div onclick="selectClay(this, ${i})">LRH</div>
                                                    <div onclick="selectClay(this, ${i})">UBQ</div>
                                                    <div onclick="selectClay(this, ${i})">OTHERS</div>
                                                </div>
                                            </div>
                                          </td>`;

                            /* ******** LOT NO TEXTBOX + BUTTON HERE ******** */
                            tableBody += `<td class="d-flex gap-0"><input name="LOT_NO" style="width:120px;"  value='${parsedData[i].LOT_NO}' />
                                        <button type="button" class ="btn btn-primary btn-sm getLot" data-castno="${parsedData[i].LOT_NO}">::</button></td>`;
                            tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-sm' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                            tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-sm' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;
                            tableBody += `<td>
                                                <select name="MUDGUN_NOZZLE" class ='form-select form-control-sm'>
                                                        <option ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''} value=""></option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                                                </select>
                                        </td>`;
                            tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-sm' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                            tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-sm' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                            tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-sm' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                            tableBody += `<td>
                                        <select name="CLAY_LEAKAGE" class ='form-select form-control-sm'>
                                    <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected' : ''} value=""></option>
                                    <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                                    <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                                </select>
                            </td>`;

                            tableBody += `<td>
                                <select name="BACK_FIRE" class ='form-select form-control-sm'>
                                    <option ${!parsedData[i].BACK_FIRE ? 'selected' : ''} value=""></option>
                                    <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                                    <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                                </select>
                            </td>`;

                            tableBody += `</tr>`;
                        }

                        $("#Mudgun_Details tbody").html(tableBody);
                    }
                });
            }
             function Display_Driling_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Driling_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Driling_Slag) {
                    var parsedData = JSON.parse(result_Driling_Slag);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {
                        tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
                        tableBody += `<td><input name="CAST_NO" class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                        tableBody += `<td><input name="DRILL_DIA" class='form-control form-control-sm' value='${parsedData[i].DRILL_DIA}'/></td>`;
                        tableBody += `<td>
                                      <select name="DRILL_TYPE" class ="form-select form-control-sm">
                                      <option value="" ${!parsedData[i].DRILL_TYPE ? 'selected' : ''}></option>
                                      <option value="LANCING" ${parsedData[i].DRILL_TYPE === 'LANCING' ? 'selected' : ''}>LANCING</option>
                                      <option value="DANGO DRILL" ${parsedData[i].DRILL_TYPE === 'DANGO DRILL' ? 'selected' : ''}>DANGO DRILL</option>
                                      <option value="SELF" ${parsedData[i].DRILL_TYPE === 'SELF' ? 'selected' : ''}>SELF</option>
                                    </select>

                                          </td>`;
                        tableBody += `<td><input name="DRILL_TIME" class='form-control form-control-sm' value='${parsedData[i].DRILL_TIME}'/></td>`;
                        tableBody += `<td><input name="NO_DRILL_BAR" class='form-control form-control-sm' value='${parsedData[i].NO_DRILL_BAR}'/></td>`;
                        tableBody += `<td><input name="NO_DRILL_BIT" class='form-control form-control-sm' value='${parsedData[i].NO_DRILL_BIT}'/></td>`;
                        tableBody += `<td><input name="NO_LANCING_PIPE" class='form-control form-control-sm' value='${parsedData[i].NO_LANCING_PIPE}'/></td>`;
                        tableBody += `<td><input name="NO_SHAFT_USED" class='form-control form-control-sm' value='${parsedData[i].NO_SHAFT_USED}'/></td>`;
                        tableBody += `<td><input name="DRILL_MC_AIR_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].DRILL_MC_AIR_PRESSURE}'/></td>`;
                        tableBody += `<td><input name="TAPHOLE_LENGTH" class='form-control form-control-sm' value='${parsedData[i].TAPHOLE_LENGTH}'/></td>`;
                        tableBody += `<td><input name="LEN_DRILL_HAMMER" class='form-control form-control-sm' value='${parsedData[i].LEN_DRILL_HAMMER}'/></td>`;
                        tableBody += `<td>
                                               <select name="COLOR_FUME_DRILLING" class ="form-select form-control-sm">
                                                <option value="" ${!parsedData[i].COLOR_FUME_DRILLING ? 'selected' : ''}></option>
                                                <option value="BROWN" ${parsedData[i].COLOR_FUME_DRILLING === 'BROWN' ? 'selected' : ''}>BROWN</option>
                                                <option value="WHITE" ${parsedData[i].COLOR_FUME_DRILLING === 'WHITE' ? 'selected' : ''}>WHITE</option>
                                                <option value="OTHERS" ${parsedData[i].COLOR_FUME_DRILLING === 'OTHERS' ? 'selected' : ''}>OTHERS</option>
                                               </select>
                                              </td>`;
                        tableBody += `<td><input name="SLAG_START_TIME" class='form-control form-control-sm' value='${parsedData[i].SLAG_START_TIME}' readonly/></td>`;
                        tableBody += `<td><input name="SLAG_TIME_RATIO" class='form-control form-control-sm' value='${parsedData[i].SLAG_TIME_RATIO}' readonly/></td>`;
                        tableBody += `<td><input name="SLAG_RETENTION" class='form-control form-control-sm' value='${parsedData[i].SLAG_RETENTION}'/></td>`;
                        tableBody += `<td><input name="SLAG_LADLE" class='form-control form-control-sm' value='${parsedData[i].SLAG_LADLE}'/></td>`;
                        tableBody += `<td><input name="NO_CINDER_GRANULATION" class='form-control form-control-sm' value='${parsedData[i].NO_CINDER_GRANULATION}'/></td>`;
                        tableBody += `<td><input name="GRANULATION_PERC" class='form-control form-control-sm' value='${parsedData[i].GRANULATION_PERC}'/></td>`;
                        tableBody += `<td><input name="CINDER_THEORETICAL_WT" class='form-control form-control-sm' value='${parsedData[i].CINDER_THEORETICAL_WT}'/></td>`;
                        tableBody += `<td><input name="SLAG_RATE" class='form-control form-control-sm' value='${parsedData[i].SLAG_RATE}'/></td>`;
                        tableBody += `<td><input name="TOTAL_SLAG" class='form-control form-control-sm' value='${parsedData[i].TOTAL_SLAG}'/></td>`;
                        tableBody += "</tr>";
                    }
                    $("#Driling_Slag_Details tbody").html(tableBody);
                },
            });
        }
             function Display_Other_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                url: '@Url.Action("Get_Display_Other_Details", "CastHouse")',
                type: 'GET',
                data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                success: function (result_Other_Details) {
                    var parsedData = JSON.parse(result_Other_Details);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {
                        tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
                        tableBody += `<td><input name="CAST_NO" class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                        tableBody += `<td><input name="MAIN_RUNNER_HM_AMOUNT" class='form-control form-control-sm' value='${parsedData[i].MAIN_RUNNER_HM_AMOUNT}'/></td>`;
                        tableBody += `<td><input name="TILT_RUNNER_HM_AMOUNT" class='form-control form-control-sm' value='${parsedData[i].TILT_RUNNER_HM_AMOUNT}'/></td>`;
                        tableBody += `<td><input name="DELAY_REASON" class='form-control form-control-sm' value='${parsedData[i].DELAY_REASON}'/></td>`;
                        tableBody += "</tr>";
                    }
                    $("#Other_Details tbody").html(tableBody);
                },
            });
        }
        function Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur) {
            $.ajax({
                url: '@Url.Action("Get_Display_Carbon_Paste_Inj", "CastHouse")',
                type: 'GET',
                data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                success: function (result_Carbon_Paste_Inj) {
                    var parsedData = JSON.parse(result_Carbon_Paste_Inj);
                    var tableBody = "";
                    if (!parsedData || parsedData.length == 0) {
                        let autoShift = getShiftFromTime(lsSelectedFDate);
                        tableBody += "<tr>";
                        tableBody += `<td><input name="DATE_TIME" class='form-control form-control-sm dt' value='${lsSelectedFDate || ""}'/></td>`;
                        tableBody += `<td>
                                <select name="SHIFT" class ="form-control form-control-sm">
                                    <option value="">Select</option>
                                    <option value="A" ${autoShift == "A" ? "selected" : ""}>A</option>
                                    <option value="B" ${autoShift == "B" ? "selected" : ""}>B</option>
                                    <option value="C" ${autoShift == "C" ? "selected" : ""}>C</option>
                              </select>
                           </td>`;
                        tableBody += `<td><input name="BELOW_TUYERE" class='form-control form-control-sm' autocomplete="off"></td>`;
                        tableBody += `<td><input name="NO_OF_DRUM"   class='form-control form-control-sm' autocomplete="off"></td>`;
                        tableBody += "</tr>";
                        $("#carbon_paste_inj tbody").html(tableBody);
                        return;
                    }
                    for (var i = 0; i < parsedData.length; i++) {
                        let finalDate = lsSelectedFDate || parsedData[i].DATE_TIME;
                        let autoShift = getShiftFromTime(finalDate);
                        let shift = parsedData[i].SHIFT || autoShift;
                        tableBody += "<tr>";
                        tableBody += `<td><input name="DATE_TIME" class='form-control form-control-sm dt' value='${finalDate}'/></td>`;
                        tableBody += `<td><select name="SHIFT"    class="form-control form-control-sm">
                                <option value="">Select</option>
                                    <option value="A" ${shift == "A" ? "selected" : ""}>A</option>
                                    <option value="B" ${shift == "B" ? "selected" : ""}>B</option>
                                    <option value="C" ${shift == "C" ? "selected" : ""}>C</option>
                                </select>
                           </td>`;
                        tableBody += `<td><input name="BELOW_TUYERE" class='form-control form-control-sm' value='${parsedData[i].BELOW_TUYERE || ""}'/></td>`;
                        tableBody += `<td><input name="NO_OF_DRUM"   class='form-control form-control-sm' value='${parsedData[i].NO_OF_DRUM || ""}'/></td>`;
                        tableBody += "</tr>";
                    }
                    $("#carbon_paste_inj tbody").html(tableBody);
                }
            });
        }
        function Display_Exception_Cast(lsSelectedFDate, IsSelectedFur) {
            $.ajax({
                url: '@Url.Action("Get_Display_Exception_Cast", "CastHouse")',
                type: 'GET',
                data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                success: function (result_Exception_Cast) {
                    var parsedData = JSON.parse(result_Exception_Cast);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {

                        tableBody += "<tr>";
                        tableBody += `<td><input name="ID_NO" class='form-control form-control-md' value='${parsedData[i].ID_NO}'/></td>`;
                        tableBody += `<td>
                                                <select name="TAPHOLE_NO" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].TAPHOLE_NO ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].TAPHOLE_NO === 1 ? 'selected' : ''}>1</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 2 ? 'selected' : ''}>2</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 3 ? 'selected' : ''}>3</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 4 ? 'selected' : ''}>4</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td><input name="DATE_TIME" class='form-control form-control-lg' value='${parsedData[i].DATE_TIME}'/></td>`;
                        tableBody += `<td>
                                                <select name="HH" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].HH ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].HH === 01 ? 'selected' : ''}>01</option>
                                                <option ${parsedData[i].HH === 02 ? 'selected' : ''}>02</option>
                                                <option ${parsedData[i].HH === 03 ? 'selected' : ''}>03</option>
                                                <option ${parsedData[i].HH === 04 ? 'selected' : ''}>04</option>
                                                <option ${parsedData[i].HH === 05 ? 'selected' : ''}>05</option>
                                                <option ${parsedData[i].HH === 06 ? 'selected' : ''}>06</option>
                                                <option ${parsedData[i].HH === 07 ? 'selected' : ''}>07</option>
                                                <option ${parsedData[i].HH === 08 ? 'selected' : ''}>08</option>
                                                <option ${parsedData[i].HH === 09 ? 'selected' : ''}>09</option>
                                                <option ${parsedData[i].HH === 10 ? 'selected' : ''}>10</option>
                                                <option ${parsedData[i].HH === 11 ? 'selected' : ''}>11</option>
                                                <option ${parsedData[i].HH === 12 ? 'selected' : ''}>12</option>
                                                <option ${parsedData[i].HH === 13 ? 'selected' : ''}>13</option>
                                                <option ${parsedData[i].HH === 14 ? 'selected' : ''}>14</option>
                                                <option ${parsedData[i].HH === 15 ? 'selected' : ''}>15</option>
                                                <option ${parsedData[i].HH === 16 ? 'selected' : ''}>16</option>
                                                <option ${parsedData[i].HH === 17 ? 'selected' : ''}>17</option>
                                                <option ${parsedData[i].HH === 18 ? 'selected' : ''}>18</option>
                                                <option ${parsedData[i].HH === 19 ? 'selected' : ''}>19</option>
                                                <option ${parsedData[i].HH === 20 ? 'selected' : ''}>20</option>
                                                <option ${parsedData[i].HH === 21 ? 'selected' : ''}>21</option>
                                                <option ${parsedData[i].HH === 22 ? 'selected' : ''}>22</option>
                                                <option ${parsedData[i].HH === 23 ? 'selected' : ''}>23</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td>
                                                <select name="MM" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].MM ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].MM === 00 ? 'selected' : ''}>00</option>
                                                <option ${parsedData[i].MM === 05 ? 'selected' : ''}>05</option>
                                                <option ${parsedData[i].MM === 10 ? 'selected' : ''}>10</option>
                                                <option ${parsedData[i].MM === 15 ? 'selected' : ''}>15</option>
                                                <option ${parsedData[i].MM === 20 ? 'selected' : ''}>20</option>
                                                <option ${parsedData[i].MM === 25 ? 'selected' : ''}>25</option>
                                                <option ${parsedData[i].MM === 30 ? 'selected' : ''}>30</option>
                                                <option ${parsedData[i].MM === 35 ? 'selected' : ''}>35</option>
                                                <option ${parsedData[i].MM === 40 ? 'selected' : ''}>40</option>
                                                <option ${parsedData[i].MM === 45 ? 'selected' : ''}>45</option>
                                                <option ${parsedData[i].MM === 50 ? 'selected' : ''}>50</option>
                                                <option ${parsedData[i].MM === 55 ? 'selected' : ''}>55</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td><input name="TAPHOLE_LENGTH" class='form-control form-control-md' value='${parsedData[i].TAPHOLE_LENGTH}'/></td>`;
                        tableBody += `<td><input name="CLAY_PUSHED" class='form-control form-control-md' value='${parsedData[i].CLAY_PUSHED}'/></td>`;
                        tableBody += `<td>
                                                <select name="TYPE" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].TYPE ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].TYPE === 'BLEEDING HOLE' ? 'selected' : ''}>BLEEDING HOLE</option>
                                                <option ${parsedData[i].TYPE === 'HOLE THROUGH' ? 'selected' : ''}>HOLE THROUGH</option>
                                                <option ${parsedData[i].TYPE === 'BLANK PUSH' ? 'selected' : ''}>BLANK PUSH</option>
                                                </select>
                                          </td>`;
                        tableBody += "</tr>";
                    }
                    $("#exception_cast tbody").html(tableBody);
                },
            });
        }



// Show dropdown
function showDropdown(btn){
    var lists = document.querySelectorAll('.mgClayList');
    for(var i=0;i<lists.length;i++){ lists[i].style.display='none'; }
    var list = btn.nextElementSibling;
    list.style.display = 'block';
    document.addEventListener('click', function handler(e){
        if(!list.contains(e.target) && e.target !== btn){
            list.style.display = 'none';
            document.removeEventListener('click', handler);
        }
    });
}

// Select item from dropdown
function selectClay(item, rowIndex){
    var list = item.parentElement;
    var input = list.previousElementSibling;
    if(item.innerText === "OTHERS"){
        $("#hdnRowIndex").val(rowIndex);
        $("#txtOtherMGClay").val(input.value); // show current value
        let modalEl = document.getElementById("mgClayOtherModal");
        let modal = new bootstrap.Modal(modalEl);
        modal.show();
    } else {
        input.value = item.innerText;
    }
    list.style.display = 'none';
}

// Save from modal
function saveOtherMGClay(){
    let rowIndex = $("#hdnRowIndex").val();
    let val = $("#txtOtherMGClay").val().trim();
    if(!val){ alert("Enter value"); return; }

    var row = document.querySelectorAll("#Mudgun_Details tbody tr")[rowIndex];
    var input = row.querySelector(".mgClayInput");
    input.value = val;

    let modalEl = document.getElementById("mgClayOtherModal");
    let modal = bootstrap.Modal.getInstance(modalEl);
    if(modal) modal.hide();
}
    </script>
    <script>
        /*******SAVE FOR CARBON PASTE INJECTION *********************/
        function saveCarbonPaste() {
            debugger;
         var url = document.getElementById("saveUrl").value;
         var rows =document.querySelectorAll("#carbon_paste_inj tbody tr");
            for (var i = 0; i < rows.length; i++) {
                var dt = rows[i].querySelector("[name='DATE_TIME']").value;
                var shift =rows[i].querySelector("[name='SHIFT']").value;
                var tuyere =rows[i].querySelector("[name='BELOW_TUYERE']").value;
                var drum =rows[i].querySelector("[name='NO_OF_DRUM']").value;
                var selectedFurnace =document.getElementById("lstFur").value.trim();
                    $.ajax({
                        url: url,
                        type: 'POST',
                        contentType:"application/x-www-form-urlencoded; charset=UTF-8",
                            data: {
                                    DATE_TIME: dt,
                                    SHIFT: shift,
                                    BELOW_TUYERE: tuyere,
                                    NO_OF_DRUM: drum,
                                    FUR: selectedFurnace
                                  },
                            success: function (res) {
                            console.log("Saved => " + res);
                        },
                    error: function (err) {
                        console.log(err);
            }
        });
    }
    alert("Carbon Paste Inj Data Saved Successfully!");
}

    </script>
    <script>
        /*********************SAVE FOR CAST HOUSE DATA *************************************/
        function SaveCastHouseData() {
            var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr,#Mudgun_Details tbody tr,#Other_Details tr");
            var CastHouseMap = {};
            rows.forEach(function (row) {
                var inputs = row.querySelectorAll("input, select");
                var castNo = "";
                var rowData = {};
                inputs.forEach(function (input) {
                    let val = input.value.trim();
                    rowData[input.name] = val === "" ? null : val;
                    if (input.name === "CAST_NO") {
                        castNo = val;
                    }
                });
                if (!CastHouseMap[castNo]) {
                    CastHouseMap[castNo] = rowData;
                } else {
                    Object.assign(CastHouseMap[castNo], rowData);
                }
            });
            var CastHouse = Object.values(CastHouseMap);
            var selectedDate = document.getElementById("tbFDatePick").value.trim();
            var selectedFurnace = document.getElementById("lstFur").value.trim();
            console.log(CastHouse);
            console.log(selectedDate);
            console.log(selectedFurnace);
            $.ajax({
                url: '/CastHouse/SaveCastHouseData',
                type: 'POST',
                contentType: 'application/json',
                data: JSON.stringify({
                    data: CastHouse,
                    Fdate: selectedDate,
                    Fur: selectedFurnace
                }),
                success: function (response) {
                    if (response.success) {
                        Swal.fire({
                            icon: 'success',
                            text: 'Data Saved Successfully!',
                            showConfirmButton: true
                        });
                    } else {
                        Swal.fire({
                            icon: 'error',
                            title: 'Failed!',
                            text: response.message || 'Data Could not be Saved.Please try again....'
                        });
                    }
                },
                error: function () {
                    Swal.fire({
                        icon: 'error',
                        title: 'Error!',
                        text: 'Something went wrong while saving.'
                    });
                }
            });
        }

    </script>
    <script>
    document.addEventListener("DOMContentLoaded", function () {
         let tbody = document.querySelector("#exception_cast tbody");
            for (let i = 0; i < 4; i++) {
                addRow();
            }
    });
    document.addEventListener("keydown", function (e) {
          if (e.key === "ArrowDown") {
                let active = document.activeElement;
                if (!active || !active.closest("#exception_cast tbody tr")) return;
                let tbody = document.querySelector("#exception_cast tbody");
                let rows = tbody.querySelectorAll("tr");
                let currentRow = active.closest("tr");
                let lastRow = rows[rows.length - 1];
                    // If cursor is in last row → add new row
                    if (currentRow === lastRow) {
                    addRow();
                    // Auto scroll to bottom
                    let wrapper = document.querySelector(".scrollable-table");
                    wrapper.scrollTop = wrapper.scrollHeight;
                    // Focus first field of new row
                    tbody.lastElementChild.querySelector("input, select").focus();
                    }
        }
    });
                        function addRow() {
                              let tbody = document.querySelector("#exception_cast tbody");
                              let tr = document.createElement("tr");
                                tr.innerHTML = `
                                            <td><input type="text" class="form-control form-control-sm"></td>
                                            <td><input type="text" class="form-control form-control-sm"></td>
                                                <td>
                                                    <select class="form-select form-select-sm">
                                                        <option></option>
                                                        <option>00</option>
                                                        <option>01</option>
                                                        <option>02</option>
                                                        <option>03</option>
                                                        <option>04</option>
                                                        <option>05</option>
                                                        <option>06</option>
                                                        <option>07</option>
                                                        <option>08</option>
                                                        <option>09</option>
                                                        <option>10</option>
                                                        <option>11</option>
                                                        <option>12</option>
                                                        <option>13</option>
                                                        <option>14</option>
                                                        <option>15</option>
                                                        <option>16</option>
                                                        <option>17</option>
                                                        <option>18</option>
                                                        <option>19</option>
                                                        <option>20</option>
                                                        <option>21</option>
                                                        <option>22</option>
                                                        <option>23</option>
                                                </select>
                                            </td>
                                     <td>
                                           <select class="form-select form-select-sm">
                                                <option></option>
                                                <option>00</option>
                                                <option>05</option>
                                                <option>10</option>
                                                <option>15</option>
                                                <option>20</option>
                                                <option>25</option>
                                                <option>30</option>
                                                <option>35</option>
                                                <option>40</option>
                                                <option>45</option>
                                                <option>50</option>
                                                <option>55</option>
                                        </select>
                                    </td>
                                        <td><input type="text" class="form-control form-control-sm"></td>
                                        <td><input type="text" class="form-control form-control-sm"></td>
                                <td>
                                        <select class="form-select form-select-sm">
                                            <option></option>
                                            <option>BLEEDING HOLE</option>
                                            <option>HOLE THROUGH</option>
                                            <option>BLANK PUSH</option>
                                        </select>
                                </td>
                            `;
                         tbody.appendChild(tr);
                    }

    </script>
</body>
</html>
