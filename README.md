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
           
            <!-- Mudgun Details -->
          
            <!--Other Details-->
          
        </div>
    </div>
    <!-- Modal for Other MG Clay -->
   
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
               

    $('#lstFur').change(function(){
        IsSelectedFur = $(this).val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
       
    });

    $('#tbFDatePick').on('changeDate', function(){
        lsSelectedFDate = $(this).val();
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

    </script>
    
</body>
</html>
