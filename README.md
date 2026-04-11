public JsonResult GetFurnaceData(string prodDate)
{
    FurnaceDataModel model = new FurnaceDataModel();

    string conString = "YOUR_CONNECTION_STRING";

    using (OracleConnection con = new OracleConnection(conString))
    {
        con.Open();

        // ================= COUNT =================
        int v_temp = 0;

        string countQuery = @"SELECT COUNT(*) 
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS')
                              AND FURNACE IN ('C','D','E','F')";

        using (OracleCommand cmd = new OracleCommand(countQuery, con))
        {
            cmd.Parameters.Add("pDate", prodDate);
            v_temp = Convert.ToInt32(cmd.ExecuteScalar());
        }

        // ================= IF =================
        if (v_temp > 0)
        {
            // -------- CURRENT --------
            string cQuery = @"SELECT ACTUAL, REPORTED, BALANCE
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS')
                              AND FURNACE = 'C'";

            using (OracleCommand cmd = new OracleCommand(cQuery, con))
            {
                cmd.Parameters.Add("pDate", prodDate);

                using (var dr = cmd.ExecuteReader())
                {
                    if (dr.Read())
                    {
                        model.ACTUAL_C = dr["ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACTUAL"]);
                        model.REPORTED_C = dr["REPORTED"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORTED"]);
                        model.BALANCE_C = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);
                    }
                }
            }

            // -------- TODATE --------
            string cTDQuery = @"SELECT 
                                DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL)),
                                DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED))
                               FROM DEMO.T_BF_PRODUCTION_TRACKING
                               WHERE TIMESTAMP >= TRUNC(TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS'),'MON')
                               AND TIMESTAMP <= TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS')
                               AND FURNACE = 'C'";

            using (OracleCommand cmd = new OracleCommand(cTDQuery, con))
            {
                cmd.Parameters.Add("pDate", prodDate);

                using (var dr = cmd.ExecuteReader())
                {
                    if (dr.Read())
                    {
                        model.ACTUAL_C_TD = dr[0] == DBNull.Value ? 0 : Convert.ToDecimal(dr[0]);
                        model.REPORTED_C_TD = dr[1] == DBNull.Value ? 0 : Convert.ToDecimal(dr[1]);
                    }
                }
            }
        }
        else
        {
            model.MESSAGE = "No Data Found";
        }
    }

    return Json(model, JsonRequestBehavior.AllowGet);
}
