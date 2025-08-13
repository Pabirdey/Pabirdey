 public JsonResult SaveCastHouseData(List<Dictionary<string, string>> data, string Fdate, string Fur)
        {
            try
            {
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();

                    string updateSql = @"
                     UPDATE TEST.T_CAST_DETAILS SET
                    ch_ready_time= :ch_ready_time, 
                    splacing_wetness_time = :splacing_wetness_time,
                    cast_type = :cast_type,
                    cast_clay_cond = :cast_clay_cond,
                    taphole_behaviour = :taphole_behaviour,
                    hm_before_slag = :hm_before_slag,
                    hm_after_slag = :hm_after_slag,
                    hm_temp = :hm_temp 
                WHERE cast_no = :cast_no 
                  AND TRUNC(DATE_TIME) = TO_DATE(:Fdate, 'DD-MM-YYYY') 
                  AND FUR_NAME = :Fur";

                    foreach (var row in data)
                    {
                        using (OracleCommand cmd = new OracleCommand(updateSql, conn))
                        {

                            cmd.Parameters.Add(":ch_ready_time", (object)row["ch_ready_time"] ??DBNull.Value);
                            cmd.Parameters.Add(":splacing_wetness_time", (object)row["splacing_wetness_time"] ?? DBNull.Value);
                            cmd.Parameters.Add(":cast_type", (object)row["cast_type"] ?? DBNull.Value);
                            cmd.Parameters.Add(":cast_clay_cond", (object)row["cast_clay_cond"] ?? DBNull.Value);
                            cmd.Parameters.Add(":taphole_behaviour", (object)row["taphole_behaviour"] ?? DBNull.Value);
                            cmd.Parameters.Add(":hm_before_slag", (object)row["hm_before_slag"] ?? DBNull.Value);
                            cmd.Parameters.Add(":hm_after_slag", (object)row["hm_after_slag"] ?? DBNull.Value);
                            cmd.Parameters.Add(":hm_temp", (object)row["hm_temp"] ?? DBNull.Value);                           
                            cmd.Parameters.Add(":cast_no", (object)row["cast_no"] ?? DBNull.Value);
                            cmd.Parameters.Add(":Fdate", Fdate);
                            cmd.Parameters.Add(":Fur", Fur);
                            cmd.ExecuteNonQuery();
                            
                        }

                    }
                }
                
                 return Json(new { success = true });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
           function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '/CastHouse/Get_TAP_Hole_Metal_Details',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Tap_Hole_Metal) {
                        var parsedData = JSON.parse(result_Tap_Hole_Metal);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {                            
                            tableBody += "<tr>";
                            tableBody += `<td><input name="cast_no" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                            tableBody += `<td><input name="trough_no" class='form-control form-control-lg' value='${parsedData[i].TROUGH_NO}' readonly/></td>`;
                            tableBody += `<td><input name="cast_st_time" class='form-control form-control-lg' value='${parsedData[i].CAST_ST_TIME}' readonly/></td>`;
                            tableBody += `<td><input name="cast_end_time" class='form-control form-control-lg' value='${parsedData[i].CAST_END_TIME}' readonly/></td>`;
                            tableBody += `<td><input name="gutko" class='form-control form-control-lg' value='${parsedData[i].GUTKO}' readonly/></td>`;
                            tableBody += `<td><input name="cast_duration" class='form-control form-control-lg' value='${parsedData[i].CAST_DURATION}' readonly/></td>`;
                            tableBody += `<td><input name="speed" class='form-control form-control-lg' value='${parsedData[i].SPEED}' readonly/></td>`;
                            tableBody += `<td><input name="no_tlc" class='form-control form-control-lg' value='${parsedData[i].NO_TLC}' readonly/></td>`;
                            tableBody += `<td><input name="no_ot" class='form-control form-control-lg' value='${parsedData[i].NO_OT}' readonly/></td>`;
                            tableBody += `<td><input name="ch_ready_time" class='form-control form-control-lg' value='${parsedData[i].CH_READY_TIME}'/></td>`;
                            tableBody += `<td><input name="splacing_wetness_time" class='form-control form-control-lg' value='${parsedData[i].SPLACING_WETNESS_TIME}'/></td>`;
                            tableBody += `<td>
                                      <select name="cast_type" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].CAST_TYPE ? 'selected': ''}></option>
                                      <option value="DRY" ${parsedData[i].CAST_TYPE === 'DRY' ? 'selected': ''}>DRY</option>
                                      <option value="NOT DRY" ${parsedData[i].CAST_TYPE === 'NOT DRY' ? 'selected': ''}>NOT DRY</option>
                                       </select></td>`;
                           tableBody += `<td>
                                      <select name="cast_clay_cond" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].CAST_CLAY_COND ? 'selected': ''}></option>
                                      <option value="WET" ${parsedData[i].CAST_CLAY_COND === 'WET' ? 'selected': ''}>WET</option>
                                      <option value="DRY" ${parsedData[i].CAST_CLAY_COND === 'DRY' ? 'selected': ''}>DRY</option>
                                      <option value="EXCESS WET" ${parsedData[i].CAST_CLAY_COND === 'EXCESS WET' ? 'selected': ''}>EXCESS WET</option>
                                      <option value="BLEEDING" ${parsedData[i].CAST_CLAY_COND === 'BLEEDING' ? 'selected': ''}>BLEEDING</option>
                                       </select></td>`;
                           tableBody += `<td>
                                      <select name="taphole_behaviour" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].TAPHOLE_BEHAVIOUR ? 'selected': ''}></option>
                                      <option value="WIDE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected': ''}>WIDE</option>
                                      <option value="NORMAL" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected': ''}>NORMAL</option>
                                      <option value="WIDE+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected': ''}>WIDE+COKE TROUBLE</option>
                                      <option value="NORMAL+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected': ''}>NORMAL+COKE TROUBLE</option>
                                       </select></td>`;
                           tableBody += `<td><input name="hm_before_slag" class='form-control form-control-lg' value='${parsedData[i].HM_BEFORE_SLAG}' /></td>`;
                           tableBody += `<td><input name="hm_after_slag" class='form-control form-control-lg'value='${parsedData[i].HM_AFTER_SLAG}' /></td>`;
                           tableBody += `<td><input name="hm_temp" class='form-control form-control-lg' value='${parsedData[i].HM_TEMP}'/></td>`;
                           tableBody += `<td><input name="hm_weight" class='form-control form-control-lg' value='${parsedData[i].HM_WEIGHT}' readonly/></td>`;
                           tableBody += "</tr>";
                        }
                        $("#TAP_Hot_Metal_Details tbody").html(tableBody);
                    }
                });
            }
              function SaveCastHouseData() {
            debugger;
             var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr");
            var CastHouse = [];
            rows.forEach(function (row) {
                var rowData = {};
                var inputs = row.querySelectorAll("input, select");
                inputs.forEach(function (input) {                    
                    rowData[input.name] = input.value.trim();
                });
                //inputs.forEach(function (input) {
                //    let val = input.value.trim();
                //    rowData[input.name] = val === "" ? null : val;
                //});
                CastHouse.push(rowData);
            });
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
                            text: 'Data Saved successfully!',
                            showConfirmButton: true,
                            customClass: {
                                popup: 'my-swal-popup', 
                                title: 'my-swal-title', 
                                htmlContainer: 'my-swal-text' 
                            }
                        });
                    } else {
                        Swal.fire({
                            icon: 'error',
                            title: 'Failed!',
                            text: 'Data could not be saved. Please try again.'
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
