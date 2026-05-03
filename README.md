  public JsonResult Get_Coke_Unloading(string date, string shift)
        {
            List<object> list = new List<object>();
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    string query = @"SELECT TIMESTAMP,SHIFT,BUNKER,C,E,F,TOTAL,BUNKER_POSITION,BALANCE FROM imtg.T_BF_CK_CONTROL_UNLOADING  WHERE TIMESTAMP = TO_DATE(:dt,'DD/MM/YYYY') ORDER BY TIMESTAMP";
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        cmd.Parameters.Add(":dt", date);
                        cmd.Parameters.Add(":shift", shift);
                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            using (OracleDataReader dr = cmd.ExecuteReader())
                            {
                                while (dr.Read())
                                {
                                    list.Add(new
                                    {
                                        TIMESTAMP = dr["TIMESTAMP"] == DBNull.Value ? null : Convert.ToDateTime(dr["TIMESTAMP"]),
                                        SHIFT = dr["SHIFT"]?.ToString(),
                                        BUNKER = dr["BUNKER"]?.ToString(),
                                        C = dr["C"]?.ToString(),
                                        E = dr["E"]?.ToString(),
                                        F = dr["F"]?.ToString(),
                                        TOTAL = dr["TOTAL"]?.ToString(),
                                        BUNKER_POSITION = dr["BUNKER_POSITION"]?.ToString(),
                                        BALANCE = dr["BALANCE"]?.ToString()
                                    });
                                }
                            }
                        }
                    }
                }

                // ✅ success
                return Json(new { success = true, data = list }, JsonRequestBehavior.AllowGet);
            }
            catch (Exception ex)
            {
                // ❗ log error (optional but recommended)
                // System.IO.File.WriteAllText("error.txt", ex.ToString());

                return Json(new
                {
                    success = false,
                    message = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }
        }
