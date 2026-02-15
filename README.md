[HttpPost]
public JsonResult GetBFRawMaterial(string furnace, string reportDate)
{
    List<Dictionary<string, object>> dataList = new List<Dictionary<string, object>>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string query = @"
        SELECT b.TAG_ID,
               b.WEB_COLUMN MATERIAL_NAME,
               CASE 
                   WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' 
                        THEN ROUND(NVL(a.VALUE,0),2)
                   WHEN b.FUR_NAME = 'F' 
                        THEN ROUND(NVL(a.VALUE,0) / 1000,2)
               END AS VALUE_TON,
               CASE 
                   WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' 
                        THEN ROUND(NVL(a.VALUE,0) * 1000,2)
                   WHEN b.FUR_NAME = 'F' 
                        THEN ROUND(NVL(a.VALUE,0),2)
               END AS VALUE_KG
        FROM imtg.T_ATOF_BIN_DETAILS b
        LEFT JOIN TEST.T_FURNACES_PROC_HM_PROD a
             ON b.TAG_ID = a.TAG_ID
            AND a.TIMESTAMP = TO_DATE(:p_date,'DD-MON-YYYY')
        WHERE b.REQUIRED = 'Y'
          AND b.WEB_COLUMN IS NOT NULL
          AND b.FUR_NAME = :p_furnace
        ORDER BY b.WEB_SL_NO";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = reportDate;
            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    Dictionary<string, object> row = new Dictionary<string, object>();

                    row["TAG_ID"] = dr["TAG_ID"];
                    row["MATERIAL_NAME"] = dr["MATERIAL_NAME"];
                    row["VALUE_TON"] = dr["VALUE_TON"] == DBNull.Value ? 0 : dr["VALUE_TON"];
                    row["VALUE_KG"] = dr["VALUE_KG"] == DBNull.Value ? 0 : dr["VALUE_KG"];

                    dataList.Add(row);
                }
            }
        }
    }

    return Json(dataList, JsonRequestBehavior.AllowGet);
}