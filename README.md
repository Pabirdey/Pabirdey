public JsonResult GetATOIBFLDReportData(string fDate)
        {
            List<BF_Production> list = new List<BF_Production>();
            string[] furnaces = { "A-F", "G", "H", "I" };
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    foreach (var furnace in furnaces)
                    {
                        BF_Production row = new BF_Production();

                        decimal LD1_TONS = 0, LD2_TONS = 0, LD3_TONS = 0;
                        decimal MRDTP_TONS = 0;

                        try
                        {
                            string countQuery = @"SELECT COUNT(*) FROM DEMO.T_LADLE WHERE TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') AND FURNACE = :FURNACE";
                            int count = 0;
                            using (OracleCommand cmd = new OracleCommand(countQuery, con))
                            {
                                cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                count = Convert.ToInt32(cmd.ExecuteScalar());
                            }
                            if (count > 0)
                            {
                                string Sql1 = @"DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL WHERE DATE_TIME = TO_DATE(:FDate,'DD/MM/YYYY') AND PLANT = :FURNACE";
                                using (OracleCommand cmd = new OracleCommand(Sql1, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                    using (var dr = cmd.ExecuteReader())
                                    {
                                        if (dr.Read())
                                        {
                                            LD1_TONS = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                                            LD2_TONS = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                                            LD3_TONS = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                                            MRDTP_TONS = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);                                           
                                        }
                                    }
                                }
                            }
                            else
                            {
                                string Sql1 = @"SELECT NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT END),0) AS LD1_TONS,NVL(SUM(CASE WHEN DESTINATION = 'LD2' THEN NET_WT END),0) AS LD2_TONS,
                                                NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT END),0) AS LD3_TONS,
                                                NVL(SUM(CASE WHEN DESTINATION='MRD' AND TRP_NO <= 50 THEN NET_WT END),0) AS MRDTP_TONS,
                                                NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END),0) AS NOOFTP
                                                FROM DEMO.T_LADLE_DETAILS WHERE LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY')+ 6/24
                                                AND LADLE_FLEND_TIME <TO_DATE(:FDate,'DD/MM/YYYY')+1+6/24 AND FUR_NAME IN ('C','D','E','F')";

                                using (OracleCommand cmd = new OracleCommand(Sql1, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;
                                }

                                
                               

                               
                            }
                        }
                        catch (Exception ex)
                        {
                            row.FURNACE = furnace;
                            row.ACT_ONDT = 0;
                            row.REPORT_ONDT = 0;
                            row.BALANCE = 0;
                            row.ACT_TODT = null;
                            row.REPORT_TODT = null;
                            System.Diagnostics.Debug.WriteLine("Error for Furnace " + furnace + ": " + ex.Message);
                            list.Add(row);
                            continue;
                        }
                        row.FURNACE = furnace;
                        row.ACT_ONDT = ACTUAL;
                        row.REPORT_ONDT = REPORTED;
                        row.BALANCE = BALANCE;
                        row.ACT_TODT = ACTUAL_TD == 0 ? (decimal?)null : ACTUAL_TD;
                        row.REPORT_TODT = REPORTED_TD == 0 ? (decimal?)null : REPORTED_TD;
                        list.Add(row);
                    }
                }
            }
            catch (Exception ex)
            {
                return Json(new
                {
                    success = false,
                    message = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
