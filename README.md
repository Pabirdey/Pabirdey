[HttpPost]
        public JsonResult SaveBFProdData(List<BFViewModel> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    foreach (var model in modelList)
                    {

                        string query1 = @"MERGE INTO TEST.T_BF_PRODUCTION_TRACKING t
                                        USING (SELECT :FURNACE AS FURNACE,:DATE_TIME AS TIMESTAMP   FROM dual) s
                                                ON (t.FURNACE = s.FURNACE AND t.TIMESTAMP = s.TIMESTAMP)
                                                WHEN MATCHED THEN
                                                UPDATE SET ACTUAL = :ACT,REPORTED = :RPT,BALANCE = :BAL
                                                WHEN NOT MATCHED THEN
                                                INSERT (FURNACE, TIMESTAMP, ACTUAL, REPORTED, BALANCE)
                                                VALUES (:FURNACE, :DATE_TIME, :ACT, :RPT, :BAL)";
                        using (OracleCommand cmd = new OracleCommand(query1, con))
                        {
                            cmd.BindByName = true;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                            cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = Convert.ToDateTime(model.DATE_TIME);
                            cmd.Parameters.Add("ACT", OracleDbType.Decimal).Value = model.ACT_ONDT;
                            cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;
                            cmd.Parameters.Add("BAL", OracleDbType.Decimal).Value = model.BALANCE;
                            cmd.ExecuteNonQuery();
                        }


                        string query2 = @"MERGE INTO TEST.T_BF_PRODUCTION_TEST t
                                                USING(SELECT :FURNACE AS FURNACE,:DATE_TIME AS TIMESTAMP FROM dual) s
                                                ON (t.FUR_NO = s.FURNACE AND t.TIMESTAMP = s.TIMESTAMP)
                                                WHEN MATCHED THEN UPDATE SET 
                                                PRODUCTION = :RPT
                                                WHEN NOT MATCHED THEN 
                                                INSERT (FUR_NO, TIMESTAMP, PRODUCTION)
                                                VALUES (:FURNACE, :DATE_TIME, :RPT)";
                        using (OracleCommand cmd = new OracleCommand(query2, con))
                        {
                            cmd.BindByName = true;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                            cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = Convert.ToDateTime(model.DATE_TIME);
                            cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;
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
 <script>
        function SaveBFProdData() {
            debugger;
            var furnaces = ["C", "E", "F", "G", "H", "I"];
            var modelList = [];
            furnaces.forEach(function (f) {
                var model = {
                    FURNACE: f,
                    DATE_TIME: lsSelectedFDate,
                    ACT_ONDT: Number($("#" + f + "_ActOnDate").val()) || 0,
                    REPORT_ONDT: Number($("#" + f + "_ReportOnDate").val()) || 0,
                    BALANCE: Number($("#" + f + "_Balance").val()) || 0
                };

                modelList.push(model);
            });
            $.ajax({
                url: '/HML/SaveBFProdData',
                type: 'POST',
                data: JSON.stringify(modelList),
                contentType: 'application/json; charset=utf-8',
                dataType: 'json',

                success: function (res) {
                    if (res.success) {
                        alert("Data Saved Successfully");
                    } else {
                        alert("Error: " + res.message);
                    }
                },
                error: function () {
                    alert("Server error");
                }
            });
        }

    </script>
