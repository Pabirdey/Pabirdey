function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {
                    var parsedData = JSON.parse(result_Mudgun_Details);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {
                        tableBody += "<tr>";
                        tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                        tableBody += `<td>
                            <select name="CLOSURE_MODE" class='form-select form-select-lg'>
                                <option ${!parsedData[i].CLOSURE_MODE ? 'selected' : ''} value=""></option>
                                <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                                <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                            </select>
                        </td>`;
                tableBody += `<td><input name="CLAY_QUANTITY" class='form-control form-control-lg' value='${parsedData[i].CLAY_QUANTITY}'/></td>`;
                tableBody += `<td>
                    <select name="MG_CLAY_USED" class='form-select form-select-lg'>
                        <option ${!parsedData[i].MG_CLAY_USED ? 'selected' : ''} value=""></option>
                        ${[
                            'ACE','BRL','LRH','UBQ','SARVESH','CALDYRS','HARIMA(S)','HARIMA(D)','CORUS','TRB','VISUVIUS',
                            'HARIMA-TWH4','HARIMA-CPH4','HARIMA(D)-TWH5','HARIMA(D)-TWH5K','HARIMA(D)-TWH-5T','HARIMA RWH-3',
                            'HARIMA RWH-4','HARIMA(S)-RW5F','HARIMA(S)-RG15K','OTHERS'
                        ].map(option => `<option ${parsedData[i].MG_CLAY_USED === option ? 'selected' : ''}>${option}</option>`).join("")}
                    </select>
                </td>`;
                tableBody += `<td><input name="LOT_NO" class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/></td>`;               
                tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-lg' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-lg' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;
                tableBody += `<td>
                    <select name="MUDGUN_NOZZLE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                        <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                    </select>
                </td>`;
                tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-lg' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                tableBody += `<td>
                    <select name="CLAY_LEAKAGE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;
                tableBody += `<td>
                    <select name="BACK_FIRE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].BACK_FIRE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;
                tableBody += "</tr>";
            }
            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
}
<html lang="en">
<head>
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">        
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" media="screen">
    <link href="@Url.Content("~/bower_components/bootstrap-daterangepicker/bootstrap-daterangepicker-1.3.21.css")" rel="stylesheet" />
    <link href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap-multiselect.css")" rel="stylesheet" />
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap-multiselect.min.css")" media="screen">
    <link href="~/bower_components/folder-explorer/font-awesome.min.css" rel="stylesheet" />
    <link href="~/bower_components/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <style>
        /*body {
            background-image: linear-gradient(90deg, #FFE259, #FFA751);
        }*/

        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }

        .my-swal-popup {
            font-family: 'Arial', sans-serif;
        }

        .my-swal-title {
            font-family: 'Georgia', serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: 'Verdana', sans-serif;
            font-size: 18px;
        }

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

        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
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

        .Long_Heading_Medium {
            min-width: 100px;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Long_Heading {
            min-width: 130px;
        }

        .section_Exception-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            width: 15vh;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

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
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        .highlight {
            background-color: #ffe08a !important;
        }

        .btnSaveCastHouse {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 10px;
            color: #FFFFFF;
            cursor: pointer;
            display: inline-block;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            font-weight: bold;
            line-height: 2.5;
            outline: transparent;
            padding: 0 1rem;
            text-align: center;
            text-decoration: none;
            transition: box-shadow .2s ease-in-out;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
            white-space: nowrap;
            width: 12vh;
            margin-left: 30px;
            margin-top: 100px;
        }

            .btnSaveCastHouse:not([disabled]):focus {
                box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
            }

            .btnSaveCastHouse:not([disabled]):hover {
                box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
            }

        .btnHMLogistics {
            margin: 10px;
            padding: 15px 30px;
            text-align: center;
            text-transform: uppercase;
            transition: 0.5s;
            background-size: 200% auto;
            color: white;
            border-radius: 10px;
            display: block;
            border: 0px;
            font-weight: bold;
            box-shadow: 0px 0px 14px -7px #f09819;
            background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
            cursor: pointer;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
        }

            .btnHMLogistics:hover {
                background-position: right center;
                color: #fff;
                text-decoration: none;
            }

            .btnHMLogistics:active {
                transform: scale(0.95);
            }

        select {
            appearance: auto !important;
            -webkit-a ppearance: auto !important;
            -moz-appearance: auto !important;
        }

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

        #backgrcol_Tap_hole {
            color: white;
            font-weight: bold;
            padding: 8px;
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
    </div>
        <div class="mt-3">
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-12">
                        <div class="section-title">Tap Hole Details/Hot Metal Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:300px;">
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
                        <div class="table-responsive scrollable-table" style="max-height:320px;">
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
                <div class="table-responsive scrollable-table" style="max-height:318px;">
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
                        <div class="table-responsive scrollable-table" style="max-height:290px;">
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
                        <div class="border rounded p-3 shadow-sm mb-4">
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <div class="section_Exception-title">Exception Cast</div>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveExceptionCast()">Save</button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:282px;">
                                <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
                                    <thead>
                                        <tr>
                                            <th style="width:100px;min-width:100px;box-sizing:border-box;">ID No</th>
                                            <th>Taphole No</th>
                                            <th style="width:150px;min-width:150px;box-sizing:border-box;">Date Time</th>
                                            <th style="width:100px;min-width:100px;box-sizing:border-box;">HH24</th>
                                            <th style="width:100px;min-width:100px;box-sizing:border-box;">MM</th>
                                            <th>Taphole Length</th>
                                            <th>Clay Paused</th>
                                            <th style="width:180px;min-width:180px;box-sizing:border-box;">Type</th>
                                        </tr>
                                    </thead>
                                    <tbody></tbody>
                                </table>
                            </div>
                        </div>
                        <!-- Carbon Paste Inj Box -->
                        <div class="border rounded p-3 shadow-sm">
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <div class="section_Exception-title">Carbon Paste Inj</div>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">Save</button>
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
                        </div>
                    </div>
                    <div class="col-md-2">
                        <div>
                            <div>
                                <div class="mb-2">
                                    <button type="button" class="btnSaveCastHouse" onclick="SaveCastHouseData()">Save</button>
                                </div>
                                @*<div>
                                        <button type="button" class="btnHMLogistics">HM Logistics</button>
                                    </div>*@
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div> 
        <div class="modal fade" id="othersModal" tabindex="-1">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title">Enter Other Clay Name</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                    </div>
                    <div class="modal-body">
                        <input type="text" id="otherClayName" class="form-control" placeholder="Enter Clay Name">
                    </div>
                    <div class="modal-footer">
                        <button type="button" id="saveOtherClay" class="btn btn-primary">Save</button>
                    </div>
                </div>
            </div>
        </div>      
</body>
</html>
 $(document).on("change", "select[name='MG_CLAY_USED']", function () {
                debugger;
                if ($(this).val() === "OTHERS") {                    
                    window.currentClayDropdown = this;                    
                    var modal = new bootstrap.Modal(document.getElementById("othersModal"));
                    modal.show();
                }
            });
