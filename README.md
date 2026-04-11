 string sqlquery = @"SELECT TRUNC(a.TIMESTAMP, 'MON') AS MONTH_START,a.TIMESTAMP,a.FUR_NAME FURNACE,NVL(SUM(a.NET_WT),0) AS ACT_ONDT,(SELECT NVL(SUM(b.ACTUAL),0) FROM DEMO.T_BF_PRODUCTION_TRACKING b WHERE b.FURNACE = a.FUR_NAME  AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP < a.TIMESTAMP) AS ACT_TODT_PREV,(SELECT NVL(SUM(b.REPORTED),0) FROM DEMO.T_BF_PRODUCTION_TRACKING b WHERE b.FURNACE = a.FUR_NAME AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP < a.TIMESTAMP) AS REPORT_TODT_PREV FROM DEMO.T_LADLE_DETAILS a WHERE a.LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY') AND a.LADLE_FLEND_TIME < TO_DATE(:FDate,'DD/MM/YYYY') AND a.DESTINATION <> 'R' GROUP BY a.FUR_NAME, a.TIMESTAMP ORDER BY a.FUR_NAME";
                    using (OracleCommand cmd = new OracleCommand(sqlquery, con))
                    {
                        cmd.Parameters.Add("pDate", fDate);
                        using (var dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                BF_Production row = new BF_Production();
                                decimal actOnDt = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);                                
                                decimal actPrev = dr["ACT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT_PREV"]);
                                decimal repPrev = dr["REPORT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT_PREV"]);                                
                                decimal ACTUAL_TD = actPrev + actOnDt;
                                decimal REPORTED_TD = repPrev + repOnDt;
                                list.Add(row);
                            }
                        }
                    }
