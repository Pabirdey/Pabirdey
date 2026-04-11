public JsonResult GetFurnaceData(string prodDate)
{
    List<FurnaceRowModel> list = new List<FurnaceRowModel>();

    string conString = "YOUR_CONNECTION_STRING";

    using (OracleConnection con = new OracleConnection(conString))
    {
        con.Open();

        // ================= COUNT =================
        int v_temp = 0;

        string countQuery = @"SELECT COUNT(*) 
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS')
                              AND FURNACE IN ('C','E','F')";

        using (OracleCommand cmd = new OracleCommand(countQuery, con))
        {
            cmd.Parameters.Add("pDate", prodDate);
            v_temp = Convert.ToInt32(cmd.ExecuteScalar());
        }

        // ================= IF COUNT > 0 =================
        if (v_temp > 0)
        {
            string query = @"
            SELECT 
                a.FURNACE,
                a.ACTUAL AS ACT_ONDT,
                a.REPORTED AS REPORT_ONDT,
                a.BALANCE,    
                (SELECT SUM(b.ACTUAL) 
                 FROM DEMO.T_BF_PRODUCTION_TRACKING b 
                 WHERE b.FURNACE = a.FURNACE 
                   AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') 
                   AND b.TIMESTAMP <= a.TIMESTAMP) AS ACT_TODT,    
                (SELECT SUM(b.REPORTED) 
                 FROM DEMO.T_BF_PRODUCTION_TRACKING b 
                 WHERE b.FURNACE = a.FURNACE 
                   AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') 
                   AND b.TIMESTAMP <= a.TIMESTAMP) AS REPORT_TODT
            FROM DEMO.T_BF_PRODUCTION_TRACKING a
            WHERE a.TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS')
            AND a.FURNACE IN ('C','E','F')
            ORDER BY a.FURNACE";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Parameters.Add("pDate", prodDate);

                using (var dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        FurnaceRowModel row = new FurnaceRowModel();

                        row.FURNACE = dr["FURNACE"].ToString();
                        row.ACT_ONDT = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);
                        row.REPORT_ONDT = dr["REPORT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_ONDT"]);
                        row.BALANCE = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);
                        row.ACT_TODT = dr["ACT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT"]);
                        row.REPORT_TODT = dr["REPORT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT"]);

                        list.Add(row);
                    }
                }
            }
        }
        else
        {
            // return empty list or message
            return Json(new { message = "No Data Found" }, JsonRequestBehavior.AllowGet);
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
