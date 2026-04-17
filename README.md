public JsonResult GetFurnaceData(string fDate)
{
    List<BF_Production> list = new List<BF_Production>();

    string[] furnaces = { "G", "H", "I" };

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        foreach (var furnace in furnaces)
        {
            BF_Production row = new BF_Production();

            decimal ACTUAL = 0, REPORTED = 0, BALANCE = 0;
            decimal ACTUAL_TD = 0, REPORTED_TD = 0;
            decimal vActual_TD = 0, vReported_TD = 0;

            // 🔹 COUNT
            string countQuery = @"SELECT COUNT(*) 
                                  FROM DEMO.T_BF_PRODUCTION_TRACKING 
                                  WHERE TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') 
                                  AND FURNACE = :FURNACE";

            int count = 0;
            using (OracleCommand cmd = new OracleCommand(countQuery, con))
            {
                cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                count = Convert.ToInt32(cmd.ExecuteScalar());
            }

            // ================= IF =================
            if (count > 0)
            {
                // 🔹 Get data
                string q1 = @"SELECT ACTUAL, REPORTED, BALANCE 
                              FROM DEMO.T_BF_PRODUCTION_TRACKING 
                              WHERE TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') 
                              AND FURNACE = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(q1, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                    using (var dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            ACTUAL = dr["ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACTUAL"]);
                            REPORTED = dr["REPORTED"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORTED"]);
                            BALANCE = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);
                        }
                    }
                }

                // 🔹 TD
                string q2 = @"SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON')
                              AND TIMESTAMP <= TO_DATE(:FDate,'DD/MM/YYYY')
                              AND FURNACE = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(q2, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                    using (var dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            ACTUAL_TD = dr.IsDBNull(0) ? 0 : dr.GetDecimal(0);
                            REPORTED_TD = dr.IsDBNull(1) ? 0 : dr.GetDecimal(1);
                        }
                    }
                }
            }

            // ================= ELSE =================
            else
            {
                // 🔹 ACTUAL
                string q1 = @"SELECT NVL(SUM(NET_WT),0)
                              FROM demo.t_ladle_details
                              WHERE LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY')+6/24
                              AND LADLE_FLEND_TIME < TO_DATE(:FDate,'DD/MM/YYYY')+1+6/24
                              AND DESTINATION <> 'R'
                              AND fur_name = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(q1, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                    ACTUAL = Convert.ToDecimal(cmd.ExecuteScalar());
                }

                // 🔹 BALANCE
                string q2 = @"SELECT NVL(SUM(ACTUAL),0) - NVL(SUM(REPORTED),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON')
                              AND TIMESTAMP < TO_DATE(:FDate,'DD/MM/YYYY')
                              AND FURNACE = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(q2, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                    BALANCE = Convert.ToDecimal(cmd.ExecuteScalar());
                }

                // 🔹 REPORTED
                REPORTED = ACTUAL + BALANCE;

                // 🔹 TD
                string q3 = @"SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON')
                              AND TIMESTAMP < TO_DATE(:FDate,'DD/MM/YYYY')
                              AND FURNACE = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(q3, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                    using (var dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            vActual_TD = dr.IsDBNull(0) ? 0 : dr.GetDecimal(0);
                            vReported_TD = dr.IsDBNull(1) ? 0 : dr.GetDecimal(1);
                        }
                    }
                }

                ACTUAL_TD = vActual_TD + ACTUAL;
                REPORTED_TD = vReported_TD + REPORTED;
            }

            // 🔹 Assign to model
            row.FURNACE = furnace;
            row.ACTUAL = ACTUAL;
            row.REPORTED = REPORTED;
            row.BALANCE = BALANCE;

            row.ACTUAL_TD = ACTUAL_TD == 0 ? (decimal?)null : ACTUAL_TD;
            row.REPORTED_TD = REPORTED_TD == 0 ? (decimal?)null : REPORTED_TD;

            list.Add(row);
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
