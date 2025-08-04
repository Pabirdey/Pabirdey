  function saveData() {
                var tapHoleData = [];
                var DrillHoleData = [];
                documnet.querySelectorAll("TAP_Hot_Metal_Details tbody tr").forEach(row=> {
                    let inputs = row.querySelectorAll("input");
                    let rowData = {};
                    inputs.forEach(input=> {
                        let name = input.name;
                        let value = input.value.trim();
                        rowData[name] = value;
                     });
                    tapHoleData.push(rowData);
                });
                $.ajex({
                    url: '/CastHouse/SaveDrillSlagSourceWise',
                    type: 'POST',
                    contentType: 'application/json',
                    data: JSON.stringify(tapHoleData),
                    success: function () {
                        alert("Data Saved Successfully!");
                    }
                });
            }

  <button type="button" class="btn btn-primary w-100" onclick="saveData()">Save</button> 

  [HttpPost]
        public JsonResult SaveDrillSlagSourceWise(List<Dictionary<string, string>> data)
        {
            
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                foreach (var row in data)
                {
                    // 1. Try to UPDATE
                    string updateSql = @"UPDATE imtg.T_CAST_DETAILS_BK SET 
                                    CH_READY_TIME=:10,
                                    SPLACING_WETNESS_TIME=:11,
                                    CAST_TYPE=:12,
                                    CAST_CLAY_COND=:13,
                                    TAPHOLE_BEHAVIOUR=:14,
                                    HM_BEFORE_SLAG=:15,
                                    HM_AFTER_SLAG=:16,
                                    HM_TEMP=:17,                                    
                                 WHERE CAST_NO = :1";

                    using (OracleCommand updateCmd = new OracleCommand(updateSql, con))
                    {
                        updateCmd.Parameters.Add(new OracleParameter("10", row["CH_READY_TIME"]));
                        updateCmd.Parameters.Add(new OracleParameter("11", row["SPLACING_WETNESS_TIME"]));
                        updateCmd.Parameters.Add(new OracleParameter("12", row["CAST_TYPE"]));
                        updateCmd.Parameters.Add(new OracleParameter("13", row["CAST_CLAY_COND"]));
                        updateCmd.Parameters.Add(new OracleParameter("14", row["TAPHOLE_BEHAVIOUR"]));
                        updateCmd.Parameters.Add(new OracleParameter("15", row["HM_BEFORE_SLAG"]));
                        updateCmd.Parameters.Add(new OracleParameter("16", row["HM_AFTER_SLAG"]));
                        updateCmd.Parameters.Add(new OracleParameter("17", row["HM_TEMP"]));

                        int rowsUpdated = updateCmd.ExecuteNonQuery();

                        // 2. If no row updated, do INSERT
                        //if (rowsUpdated == 0)
                        //{
                        //    string insertSql = @"INSERT INTO IMTG.T_CAST_DETAILS_BK 
                        //                (CH_READY_TIME, DRILL_DIA, DRILL_TYPE, DRILL_TIME, BARS, SLAG_START, SLAG_RATIO, GRANULATION)
                        //                VALUES (:1, :2, :3, :4, :5, :6, :7, :8)";
                        //    using (OracleCommand insertCmd = new OracleCommand(insertSql, con))
                        //    {
                        //        insertCmd.Parameters.Add(new OracleParameter("1", row["CastNo"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("2", row["DrillDia"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("3", row["DrillType"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("4", row["DrillTime"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("5", row["Bars"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("6", row["SlagStart"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("7", row["SlagRatio"]));
                        //        insertCmd.Parameters.Add(new OracleParameter("8", row["Granulation"]));
                        //        insertCmd.ExecuteNonQuery();
                        //    }
                        //}
                    }
                }
            }

            return Json("Success");
        }

            
