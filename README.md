public JsonResult GetCTOFBFReportDataByFurnace(string fDate,decimal ? repOnDt)
        {
            List<BF_Production> list = new List<BF_Production>();
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                // ================= COUNT =================
                int v_temp = 0;
                string countQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_BALANCE WHERE TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') AND FURNACE IN ('C','E','F')";
                using (OracleCommand cmd = new OracleCommand(countQuery, con))
                {
                    cmd.Parameters.Add("pDate", fDate);
                    v_temp = Convert.ToInt32(cmd.ExecuteScalar());
                }
                // ================= IF COUNT > 0 =================
                if (v_temp > 0)
                {
                    string query = @"SELECT a.FURNACE,a.ACTUAL AS ACT_ONDT,a.REPORTED AS REPORT_ONDT,a.BALANCE,(SELECT SUM(b.ACTUAL) FROM DEMO.T_BF_PRODUCTION_BALANCE b  WHERE b.FURNACE = a.FURNACE  AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')  AND b.TIMESTAMP <= a.TIMESTAMP) AS ACT_TODT,(SELECT SUM(b.REPORTED) FROM DEMO.T_BF_PRODUCTION_BALANCE b WHERE b.FURNACE = a.FURNACE AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP <= a.TIMESTAMP) AS REPORT_TODT FROM DEMO.T_BF_PRODUCTION_BALANCE a WHERE a.TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') ORDER BY a.FURNACE";
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        cmd.Parameters.Add("pDate", fDate);

                        using (var dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                BF_Production row = new BF_Production();
                                row.FURNACE = dr["FURNACE"].ToString();
                                row.ACT_ONDT = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);
                                row.ACT_TODT = dr["ACT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT"]);
                                row.REPORT_ONDT = dr["REPORT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_ONDT"]);
                                row.REPORT_TODT = dr["REPORT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT"]);
                                row.BALANCE = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);                                                             
                                list.Add(row);
                            }
                        }
                    }
                }
                else
                {                    
                    string sqlquery = @"SELECT TRUNC(a.TIMESTAMP, 'MON') AS MONTH_START,a.TIMESTAMP,a.FUR_NAME FURNACE,NVL(SUM(a.NET_WT),0) AS ACT_ONDT,(SELECT NVL(SUM(b.ACTUAL),0) FROM DEMO.T_BF_PRODUCTION_BALANCE b WHERE b.FURNACE = a.FUR_NAME  AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP < a.TIMESTAMP) AS ACT_TODT_PREV,(SELECT NVL(SUM(b.REPORTED),0) FROM DEMO.T_BF_PRODUCTION_BALANCE b WHERE b.FURNACE = a.FUR_NAME AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP < a.TIMESTAMP) AS REPORT_TODT_PREV FROM DEMO.T_LADLE_DETAILS a WHERE a.LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY')+6/24 AND a.LADLE_FLEND_TIME < TO_DATE(:FDate,'DD/MM/YYYY')+1+6/24 AND a.DESTINATION <> 'R' GROUP BY a.FUR_NAME, a.TIMESTAMP ORDER BY a.FUR_NAME";
                    using (OracleCommand cmd = new OracleCommand(sqlquery, con))
                    {
                        cmd.Parameters.Add("pDate", fDate);
                        using (var dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                BF_Production row = new BF_Production();
                                 row.FURNACE = dr["FURNACE"].ToString();
                                 row.ACT_ONDT = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);                                
                                 row.ACT_TODT_PREV = dr["ACT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT_PREV"]);
                                 row.REPORT_TODT = dr["REPORT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT_PREV"]);
                                 row.REPORT_ONDT = repOnDt ?? 0;
                                 row.ACTUAL_TD = row.ACT_TODT + row.ACT_ONDT;
                                decimal REPORTED_TD = repPrev + repOnDtVal;
                                list.Add(row);
                            }
                        }
                    }
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
