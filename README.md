[HttpPost]
public JsonResult GetTagData(string furnace)
{
    List<Dictionary<string, object>> dataList =
        new List<Dictionary<string, object>>();

    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string query = @"
            SELECT a.WEB_SL_NO,
                   a.FUR_NAME,
                   b.TAG_NAME AS HISTORIAN_TAG_NAME,
                   a.WEB_COLUMN,
                   b.TAG_TYPE,
                   a.REQUIRED
            FROM imtg.T_ATOF_BIN_DETAILS a,
                 imtg.T_ATOF_PRODUCTION_TAG_MASTER b
            WHERE a.TAG_ID = b.TAG_ID
              AND a.FUR_NAME = :FURNACE
              AND a.WEB_SL_NO IS NOT NULL
              AND a.WEB_COLUMN IS NOT NULL
            ORDER BY a.WEB_SL_NO";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("FURNACE", furnace);

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    Dictionary<string, object> row =
                        new Dictionary<string, object>();

                    row["WEB_SL_NO"] = dr["WEB_SL_NO"].ToString();
                    row["WEB_COLUMN"] = dr["WEB_COLUMN"].ToString();
                    row["TAG_TYPE"] = dr["TAG_TYPE"].ToString();
                    row["REQUIRED"] = dr["REQUIRED"].ToString();

                    dataList.Add(row);
                }
            }
        }
    }

    return Json(dataList, JsonRequestBehavior.AllowGet);
}