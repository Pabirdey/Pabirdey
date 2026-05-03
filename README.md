public JsonResult GetFinesTrend(string type, string value)
{
    List<object> list = new List<object>();

    string connStr = ConfigurationManager.ConnectionStrings["OracleConn"].ConnectionString;

    using (OracleConnection con = new OracleConnection(connStr))
    {
        con.Open();

        string column = "";

        // Map clicked element to DB column
        switch (type.ToUpper())
        {
            case "AL2O3":
                column = "RETURN_FINES_AL2O3";
                break;

            case "SIO2":
                column = "RETURN_FINES_SIO2";
                break;

            case "P":
                column = "RETURN_FINES_P";
                break;

            case "K2O":
                column = "RETURN_FINES_K2O";
                break;

            default:
                column = "RETURN_FINES_AL2O3";
                break;
        }

        string query = $@"
            SELECT 
                TRUNC(TIMESTAMP) AS TREND_DATE,
                {column} AS VALUE
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE TRUNC(TIMESTAMP) >= TRUNC(SYSDATE - 30)
            ORDER BY TIMESTAMP";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(new
                    {
                        DATE = Convert.ToDateTime(dr["TREND_DATE"]).ToString("yyyy-MM-dd"),
                        VALUE = dr["VALUE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["VALUE"])
                    });
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
