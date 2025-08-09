   function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
             $.ajax({
                    url: '/CastHouse/Get_TAP_Hole_Metal_Details', 
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Tap_Hole_Metal) {
                        var parsedData = JSON.parse(result_Tap_Hole_Metal);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {
                            var data = parsedData[i];
                            tableBody += "<tr>";
                            tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${data.CAST_NO || ''}' readonly/></td>`;
                            tableBody += `<td><input name="TROUGH_NO" class='form-control form-control-lg' value='${data.TROUGH_NO || ''}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_ST_TIME" class='form-control form-control-lg' value='${data.CAST_ST_TIME || ''}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_END_TIME" class='form-control form-control-lg' value='${data.CAST_END_TIME || ''}' readonly/></td>`;
                            tableBody += `<td><input name="GUTKO" class='form-control form-control-lg' value='${data.GUTKO || ''}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_DURATION" class='form-control form-control-lg' value='${data.CAST_DURATION || ''}' readonly/></td>`;
                            tableBody += `<td><input name="SPEED" class='form-control form-control-lg' value='${data.SPEED || ''}' readonly/></td>`;
                            tableBody += `<td><input name="NO_TLC" class='form-control form-control-lg' value='${data.NO_TLC || ''}' readonly/></td>`;
                            tableBody += `<td><input name="NO_OT" class='form-control form-control-lg' value='${data.NO_OT || ''}' readonly/></td>`;
                            tableBody += `<td><input type="text" name="CH_READY_TIME" class='form-control form-control-lg' value='${data.CH_READY_TIME || ''}' /></td>`;
                            tableBody += `<td><input type="text" name="SPLACING_WETNESS_TIME" class='form-control form-control-lg' value='${data.SPLACING_WETNESS_TIME || ''}' /></td>`;
                            tableBody += `<td><select name="CAST_TYPE" class='form-select form-select-lg'>
                                <option ${data.CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option>
                                <option ${data.CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
                              </select></td>`;
                            tableBody += `<td><select name="CAST_CLAY_COND" class='form-select form-select-lg'>
                                <option value="" ${!data.CAST_CLAY_COND ? 'selected' : ''}></option>
                                <option ${data.CAST_CLAY_COND === 'WET' ? 'selected': ''}style="font-weight:bold;">WET</option>
                                <option ${data.CAST_CLAY_COND === 'DRY' ? 'selected': ''}style="font-weight:bold;">DRY</option>
                                <option ${data.CAST_CLAY_COND === 'EXCESS WET' ? 'selected': ''}style="font-weight:bold;">EXCESS WET</option>
                                <option ${data.CAST_CLAY_COND === 'BLEEDING' ? 'selected': ''}style="font-weight:bold;">BLEEDING</option>
                              </select></td>`;
                            tableBody += `<td><select name="TAPHOLE_BEHAVIOUR" class='form-select form-select-lg'>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected' : ''}>WIDE</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected' : ''}>NORMAL</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected' : ''}>NORMAL+COKE TROUBLE</option>
                              </select></td>`;
                              tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control form-control-lg' value='${data.HM_BEFORE_SLAG || ''}' /></td>`;
                              tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control form-control-lg' value='${data.HM_AFTER_SLAG || ''}' /></td>`;
                              tableBody += `<td><input name="HM_TEMP" class='form-control form-control-lg' value='${data.HM_TEMP || ''}' /></td>`;
                              tableBody += `<td><input name="HM_WEIGHT" class='form-control form-control-lg' value='${data.HM_WEIGHT || ''}' readonly/></td>`;
                        tableBody += "</tr>";
            }
            $("#TAP_Hot_Metal_Details tbody").html(tableBody);
        }       
    });
}


        [HttpPost]
        public JsonResult SaveCastHouseData(List<Dictionary<string, string>> data, string Fdate, string Fur)
        {
            try
            {
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();

                    string updateSql = @"
                UPDATE TEST.T_CAST_DETAILS SET
                    CH_READY_TIME = :CH_READY_TIME,
                    SPLICING_WETNESS_TIME = :SPLICING_WETNESS_TIME,
                    CAST_TYPE = :CAST_TYPE,
                    CAST_CLAY_COND = :CAST_CLAY_COND,
                    TAPHOLE_BEHAVIOUR = :TAPHOLE_BEHAVIOUR,
                    HM_BEFORE_SLAG = :HM_BEFORE_SLAG,
                    HM_AFTER_SLAG = :HM_AFTER_SLAG,
                    HM_TEMP = :HM_TEMP
                WHERE CAST_NO = :CAST_NO
                  AND DATE_TIME =TO_DATE('" + Fdate + "', 'DD-MM-YYYY')  AND  FUR_NAME = '" + Fur + "'";

                    foreach (var row in data)
                    {
                        using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                        {
                            // Bind parameters from row data
                            updateCmd.Parameters.Add(":CH_READY_TIME", row["CH_READY_TIME"]);
                            updateCmd.Parameters.Add(":SPLICING_WETNESS_TIME", row["SPLICING_WETNESS_TIME"]);
                            updateCmd.Parameters.Add(":CAST_TYPE", row["CAST_TYPE"]);
                            updateCmd.Parameters.Add(":CAST_CLAY_COND", row["CAST_CLAY_COND"]);
                            updateCmd.Parameters.Add(":TAPHOLE_BEHAVIOUR", row["TAPHOLE_BEHAVIOUR"]);
                            updateCmd.Parameters.Add(":HM_BEFORE_SLAG", row["HM_BEFORE_SLAG"]);
                            updateCmd.Parameters.Add(":HM_AFTER_SLAG", row["HM_AFTER_SLAG"]);
                            updateCmd.Parameters.Add(":HM_TEMP", row["HM_TEMP"]);

                            // CAST_NO should come from the row
                            updateCmd.Parameters.Add(":CAST_NO", row["CAST_NO"]);

                            // Use parameters for these too
                            updateCmd.Parameters.Add(":DATE_TIME", Fdate);
                            updateCmd.Parameters.Add(":FUR_NAME", Fur);

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
