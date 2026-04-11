public JsonResult GetFurnaceData()
{
    var result = new List<object>();

    string conStr = ConfigurationManager.ConnectionStrings["OracleDB"].ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        string query = @"
        SELECT 
            TRUNC(a.TIMESTAMP, 'MON') AS MONTH_START,
            a.TIMESTAMP,
            a.FUR_NAME,
            NVL(SUM(a.NET_WT),0) AS ACT_ONDT,

            (SELECT NVL(SUM(b.ACTUAL),0)
             FROM DEMO.T_BF_PRODUCTION_TRACKING b
             WHERE b.FURNACE = a.FUR_NAME
             AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')
             AND b.TIMESTAMP < a.TIMESTAMP) AS ACT_TODT,

            (SELECT NVL(SUM(b.REPORTED),0)
             FROM DEMO.T_BF_PRODUCTION_TRACKING b
             WHERE b.FURNACE = a.FUR_NAME
             AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')
             AND b.TIMESTAMP < a.TIMESTAMP) AS REPORT_TODT

        FROM DEMO.T_LADLE_DETAILS a
        WHERE a.LADLE_FLEND_TIME >= TO_DATE(:fromDate,'DD-MON-YYYY HH24:MI:SS')
        AND a.LADLE_FLEND_TIME < TO_DATE(:toDate,'DD-MON-YYYY HH24:MI:SS')
        AND a.DESTINATION <> 'R'
        GROUP BY a.FUR_NAME, a.TIMESTAMP
        ORDER BY a.FUR_NAME";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            // 🔹 Pass dates as string (same as your query)
            cmd.Parameters.Add("fromDate", OracleDbType.Varchar2)
                .Value = "10-APR-2026 06:00:00";

            cmd.Parameters.Add("toDate", OracleDbType.Varchar2)
                .Value = "11-APR-2026 06:00:00";

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    result.Add(new
                    {
                        MONTH_START = dr["MONTH_START"].ToString(),
                        TIMESTAMP = dr["TIMESTAMP"].ToString(),
                        FUR_NAME = dr["FUR_NAME"].ToString(),
                        ACT_ONDT = dr["ACT_ONDT"].ToString(),
                        ACT_TODT = dr["ACT_TODT"].ToString(),
                        REPORT_TODT = dr["REPORT_TODT"].ToString()
                    });
                }
            }
        }
    }

    return Json(result, JsonRequestBehavior.AllowGet);
}
