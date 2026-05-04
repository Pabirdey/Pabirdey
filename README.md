public JsonResult GetFinesTrend(string type, string element)
{
    List<object> list = new List<object>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        // सुरक्षा
        var allowed = new List<string> { "AL2O3", "SIO2", "P", "K2O" };
        if (!allowed.Contains(element.ToUpper()))
        {
            element = "AL2O3";
        }

        string column = "";

        switch (type.ToUpper())
        {
            case "RETURN_FINES":
                column = $"RETURN_FINES_{element}";
                break;

            case "WET_FINES":
                column = $"WET_FINES_{element}";
                break;

            case "DRY_FINES":
                column = $"DRY_FINES_{element}";
                break;

            case "DRY_FINES_500TPH":
                column = $"DRY_FINES_500TPH_{element}";
                break;
        }

        string query = $@"
        SELECT TRUNC(TIMESTAMP) TREND_DATE,
               NVL({column},0) VALUE
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
                    DATE = Convert.ToDateTime(dr["TREND_DATE"]).ToString("dd-MM-yyyy"),
                    VALUE = Convert.ToDecimal(dr["VALUE"])
                });
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
