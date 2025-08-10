  [HttpPost]
        public JsonResult SaveCastHouseData(List<Dictionary<string, string>> data, string Fdate, string Fur)
        {
            try
            {
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();

                    string updateSql = @"UPDATE TEST.T_CAST_DETAILS SET         
                    DRILL_DIA=:DRILL_DIA,DRILL_TYPE=:DRILL_TYPE,
                    DRILL_TIME=:DRILL_TIME,NO_DRILL_BAR=:NO_DRILL_BAR,NO_DRILL_BIT=:NO_DRILL_BIT,NO_LANCING_PIPE=:NO_LANCING_PIPE,
                    NO_SHAFT_USED=:NO_SHAFT_USED,DRILL_MC_AIR_PRESSURE=:DRILL_MC_AIR_PRESSURE,TAPHOLE_LENGTH=:TAPHOLE_LENGTH,
                    LEN_DRILL_HAMMER=:LEN_DRILL_HAMMER,COLOR_FUME_DRILLING=:COLOR_FUME_DRILLING,SLAG_RETENTION=:SLAG_RETENTION,
                    SLAG_LADLE=:SLAG_LADLE,NO_CINDER_GRANULATION=:NO_CINDER_GRANULATION,GRANULATION_PERC=:GRANULATION_PERC,
                    CINDER_THEORETICAL_WT=:CINDER_THEORETICAL_WT,SLAG_RATE=:SLAG_RATE,TOTAL_SLAG=:TOTAL_SLAG
                    WHERE CAST_NO = :CAST_NO AND DATE_TIME = TO_DATE(:Fdate, 'DD-MM-YYYY') AND FUR_NAME = :Fur";

                    
                    foreach (var row in data)
                    {
                        using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                        {
                           
                            updateCmd.Parameters.Add(":DRILL_DIA", row["DRILL_DIA"]);
                            updateCmd.Parameters.Add(":DRILL_TYPE", row["DRILL_TYPE"]);
                            updateCmd.Parameters.Add(":DRILL_TIME", row["DRILL_TIME"]);
                            updateCmd.Parameters.Add(":NO_DRILL_BAR", row["NO_DRILL_BAR"]);
                            updateCmd.Parameters.Add(":NO_DRILL_BIT", row["NO_DRILL_BIT"]);
                            updateCmd.Parameters.Add(":NO_LANCING_PIPE", row["NO_LANCING_PIPE"]);
                            updateCmd.Parameters.Add(":NO_SHAFT_USED", row["NO_SHAFT_USED"]);
                            updateCmd.Parameters.Add(":DRILL_MC_AIR_PRESSURE", row["DRILL_MC_AIR_PRESSURE"]);
                            updateCmd.Parameters.Add(":TAPHOLE_LENGTH", row["TAPHOLE_LENGTH"]);
                            updateCmd.Parameters.Add(":LEN_DRILL_HAMMER", row["LEN_DRILL_HAMMER"]);
                            updateCmd.Parameters.Add(":COLOR_FUME_DRILLING", row["COLOR_FUME_DRILLING"]);                           
                            updateCmd.Parameters.Add(":SLAG_RETENTION", row["SLAG_RETENTION"]);
                            updateCmd.Parameters.Add(":SLAG_LADLE", row["SLAG_LADLE"]);
                            updateCmd.Parameters.Add(":NO_CINDER_GRANULATION", row["NO_CINDER_GRANULATION"]);
                            updateCmd.Parameters.Add(":GRANULATION_PERC", row["GRANULATION_PERC"]);
                            updateCmd.Parameters.Add(":CINDER_THEORETICAL_WT", row["CINDER_THEORETICAL_WT"]);
                            updateCmd.Parameters.Add(":SLAG_RATE", row["SLAG_RATE"]);
                            updateCmd.Parameters.Add(":TOTAL_SLAG", row["TOTAL_SLAG"]);                            
                            updateCmd.Parameters.Add(":CAST_NO", row["CAST_NO"]);
                            updateCmd.Parameters.Add(":Fdate", Fdate);
                            updateCmd.Parameters.Add(":Fur", Fur);
                            updateCmd.ExecuteNonQuery();
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

        function Display_Driling_Details(lsSelectedFDate,IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Driling_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Driling_Slag) {
                        var parsedData = JSON.parse(result_Driling_Slag);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {
                            tableBody += "<tr>";
                            tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                            tableBody += `<td><input name="DRILL_DIA" class='form-control form-control-lg' value='${parsedData[i].DRILL_DIA}'/></td>`;
                            tableBody += `<td>
                                      <select name="DRILL_TYPE" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].DRILL_TYPE ? 'selected': ''}></option>
                                      <option value="LANCING" ${parsedData[i].DRILL_TYPE === 'LANCING' ? 'selected': ''}>LANCING</option>
                                      <option value="DANGO DRILL" ${parsedData[i].DRILL_TYPE === 'DANGO DRILL' ? 'selected': ''}>DANGO DRILL</option>
                                      <option value="SELF" ${parsedData[i].DRILL_TYPE === 'SELF' ? 'selected': ''}>SELF</option>
                                    </select>

                                          </td>`;
                            tableBody += `<td><input name="DRILL_TIME" class='form-control form-control-lg' value='${parsedData[i].DRILL_TIME}'/></td>`;
                            tableBody += `<td><input name="NO_DRILL_BAR" class='form-control form-control-lg' value='${parsedData[i].NO_DRILL_BAR}'/></td>`;
                            tableBody += `<td><input name="NO_DRILL_BIT" class='form-control form-control-lg' value='${parsedData[i].NO_DRILL_BIT}'/></td>`;
                            tableBody += `<td><input name="NO_LANCING_PIPE" class='form-control form-control-lg' value='${parsedData[i].NO_LANCING_PIPE}'/></td>`;
                            tableBody += `<td><input name="NO_SHAFT_USED" class='form-control form-control-lg' value='${parsedData[i].NO_SHAFT_USED}'/></td>`;
                            tableBody += `<td><input name="DRILL_MC_AIR_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].DRILL_MC_AIR_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="TAPHOLE_LENGTH" class='form-control form-control-lg' value='${parsedData[i].TAPHOLE_LENGTH}'/></td>`;
                            tableBody += `<td><input name="LEN_DRILL_HAMMER" class='form-control form-control-lg' value='${parsedData[i].LEN_DRILL_HAMMER}'/></td>`;
                            tableBody += `<td>
                                               <select name="COLOR_FUME_DRILLING" class ="form-select form-select-lg">
                                                <option value="" ${!parsedData[i].COLOR_FUME_DRILLING ? 'selected': ''}></option>
                                                <option value="BROWN" ${parsedData[i].COLOR_FUME_DRILLING === 'BROWN' ? 'selected': ''}>BROWN</option>
                                                <option value="WHITE" ${parsedData[i].COLOR_FUME_DRILLING === 'WHITE' ? 'selected': ''}>WHITE</option>
                                                <option value="OTHERS" ${parsedData[i].COLOR_FUME_DRILLING === 'OTHERS' ? 'selected': ''}>OTHERS</option>
                                               </select>
                                              </td>`;
                            tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].SLAG_START_TIME}' readonly/></td>`;
                            tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].SLAG_TIME_RATIO}' readonly/></td>`;
                            tableBody += `<td><input name="SLAG_RETENTION" class='form-control form-control-lg' value='${parsedData[i].SLAG_RETENTION}'/></td>`;
                            tableBody += `<td><input name="SLAG_LADLE" class='form-control form-control-lg' value='${parsedData[i].SLAG_LADLE}'/></td>`;
                            tableBody += `<td><input name="NO_CINDER_GRANULATION" class='form-control form-control-lg' value='${parsedData[i].NO_CINDER_GRANULATION}'/></td>`;
                            tableBody += `<td><input name="GRANULATION_PERC" class='form-control form-control-lg' value='${parsedData[i].GRANULATION_PERC}'/></td>`;
                            tableBody += `<td><input name="CINDER_THEORETICAL_WT" class='form-control form-control-lg' value='${parsedData[i].CINDER_THEORETICAL_WT}'/></td>`;
                            tableBody += `<td><input name="SLAG_RATE" class='form-control form-control-lg' value='${parsedData[i].SLAG_RATE}'/></td>`;
                            tableBody += `<td><input name="TOTAL_SLAG" class='form-control form-control-lg' value='${parsedData[i].TOTAL_SLAG}'/></td>`;
                            tableBody += "</tr>";
                        }
                        $("#Driling_Slag_Details tbody").html(tableBody);
                    },
                });
            }
