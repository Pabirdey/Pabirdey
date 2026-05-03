public JsonResult GetFinesTrend(string type)
{
    List<object> list = new List<object>();

    using (OracleConnection con = new OracleConnection(mycon))
    {
        con.Open();

        string column = "";

        switch (type.ToUpper())
        {
            case "RETURN_FINES":
                column = "RETURN_FINES_AL2O3";
                break;

            case "WET_FINES":
                column = "WET_FINES_AL2O3";
                break;

            case "DRY_FINES":
                column = "DRY_FINES_AL2O3";
                break;

            case "DRY_FINES_500TPH":
                column = "DRY_FINES_500TPH_AL2O3";
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
        WHERE TIMESTAMP >= SYSDATE - 30
        ORDER BY TIMESTAMP";

        using (OracleCommand cmd = new OracleCommand(query, con))
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

    return Json(list, JsonRequestBehavior.AllowGet);
}
