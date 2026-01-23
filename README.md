<!DOCTYPE html>
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
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }
        .scrollable-table {
    max-height: 318px;
    overflow-x: auto;
    overflow-y: auto;
    position: relative;
}

/* Freeze Cast No column horizontally */
#Mudgun_Details th:first-child,
#Mudgun_Details td:first-child {
    position: sticky;
    left: 0;
    background: #ffffff;
    z-index: 3;
    min-width: 120px;
}

/* Keep header above body */
#Mudgun_Details thead th:first-child {
    background: #f8f9fa;
    z-index: 5;
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
            border: 5px solid;
        }

        .Long_Heading_Medium {
            min-width: 100px;
            border: 1px solid black;
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

        fieldset {
            border: 2px solid #ccc !important;
            padding: 10px 12px 12px 12px;
        }

        legend {
            font-size: 24px;
            font-weight: 800;
            padding: 0 8px;
        }

        .input-wrapper {
            display: flex;
            border: 1px solid #999;
        }

            .input-wrapper input {
                border: none;
                outline: none;
            }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            border: 1px solid #999;
            display: none;
            background: #fff;
            position: absolute;
            z-index: 999;
        }

            .list-box div {
                padding: 5px;
                cursor: pointer;
            }

                .list-box div:hover {
                    background: #e6e6e6;
                }

        .input-wrapper {
            position: relative;
        }

        .arrow-btn {
            position: absolute;
            right: 5px;
            top: 6px;
            cursor: pointer;
            user-select: none;
        }

        .list-box {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            width: 100%;
            max-height: 200px;
            overflow-y: auto;
            z-index: 9999;
        }

            .list-box div {
                padding: 6px;
                cursor: pointer;
            }

                .list-box div:hover {
                    background: #f0f0f0;
                }
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
        <div class="mt-1">           
          
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
         
        </div>
    </div>   
    <!-- ================= MODAL ================= -->
    <div class="modal fade" id="mgClayOtherModal" tabindex="-1">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Other MG Clay Type</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <label class="form-label">Enter MG Clay Type</label>
                    <input type="text"
                           id="txtOtherMGClay"
                           class="form-control form-control-lg"
                           placeholder="Enter value">
                    <input type="hidden" id="hdnRowIndex">
                </div>
                <div class="modal-footer">
                    <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                    <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
                </div>
            </div>
        </div>
    </div> 
</body>
</html>
@section scripts {
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-daterangepicker/bootstrap-daterangepicker-1.3.21.js")"></script>  
    <script src="~/bower_components/bootstrap-timepicker/js/bootstrap-timepicker.js"></script>
    <script src="~/bower_components/sweetalert/dist/Swwt2Alert.js"></script>
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script type="text/javascript">
    let lsSelectedFDate;
    let IsSelectedFur;

    $(document).ready(function () {

        lsSelectedFDate = '@DateTime.Today.ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

        $('#tbFDatePick').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).val(lsSelectedFDate);

        $('#tbFDatePick').on('changeDate', function () {
            lsSelectedFDate = $('#tbFDatePick').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

        $('#lstFur').change(function () {
            IsSelectedFur = $('#lstFur option:selected').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

    });

        $(document).ready(function () {

        lsSelectedFDate = '@DateTime.Today.ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

        $('#tbFDatePick').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).val(lsSelectedFDate);

        $('#tbFDatePick').on('changeDate', function () {
            lsSelectedFDate = $('#tbFDatePick').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

        $('#lstFur').change(function () {
            IsSelectedFur = $('#lstFur option:selected').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

    });


           function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
                 $.ajax({
                 url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                 type: 'GET',
                 data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                 success: function (result_Mudgun_Details) {
                    var parsedData = JSON.parse(result_Mudgun_Details);
                    var tableBody = "";
            for (var i = 0; i < parsedData.length; i++) {
                tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
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
                            <div class="input-wrapper"><input type="text" class="form-control form-control-lg" id="clayInput_${i}" name="MG_CLAY_USED">
                                <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                                    <div class="list-box" id="list_${i}">
                                    <div onclick="selectItem(this, ${i})">ACE</div>
                                    <div onclick="selectItem(this, ${i})">BRL</div>
                                    <div onclick="selectItem(this, ${i})">LRH</div>
                                    <div onclick="selectItem(this, ${i})">UBQ</div>
                                    <div onclick="selectItem(this, ${i})">SARVESH</div>
                                    <div onclick="selectItem(this, ${i})">OTHERS</div>
                                </div>
                            </div>
                        </td>`;
                /* ******** LOT NO TEXTBOX + BUTTON HERE ******** */
                tableBody += `
<td class="d-flex gap-0">
    <input name="LOT_NO" style="width:120px;" value="${parsedData[i].LOT_NO}" />
    <button type="button"
            class="btn btn-primary btn-sm getLot"
            data-castno="${parsedData[i].LOT_NO}">
        ::
    </button>
</td>`;

                tableBody += `
<td>
    <input name="NO_OF_BAGS"
           class="form-control form-control-lg"
           value="${parsedData[i].NO_OF_BAGS}" />
</td>`;

                tableBody += `
<td>
    <input name="MUDGUN_HOLD_TIME"
           class="form-control form-control-lg"
           value="${parsedData[i].MUDGUN_HOLD_TIME}" />
</td>`;

                tableBody += `
<td>
    <select name="MUDGUN_NOZZLE" class="form-select form-select-lg">
        <option value="" ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''}></option>
        <option value="REPLACEMENT"
            ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>
            REPLACEMENT
        </option>
        <option value="WEILD"
            ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>
            WEILD
        </option>
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





</script>
    
}
