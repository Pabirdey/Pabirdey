public JsonResult GetFurnaceData(string furNo)
{
    string conStr = ConfigurationManager.ConnectionStrings["OracleDB"].ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        string query = @"SELECT COAL_TYPE, IO_TYPE, PYROXINITE_TYPE, LIMESTONE_TYPE
                         FROM DEMO.T_BF_PRODUCTION_TEST
                         WHERE TIMESTAMP = (
                            SELECT MAX(TIMESTAMP)
                            FROM DEMO.T_BF_PRODUCTION_TEST
                            WHERE FUR_NO = :furNo
                            AND IO_TYPE IS NOT NULL)
                         AND FUR_NO = :furNo";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("furNo", furNo);

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                if (dr.Read())
                {
                    return Json(new
                    {
                        COAL_TYPE = dr["COAL_TYPE"].ToString(),
                        IO_TYPE = dr["IO_TYPE"].ToString(),
                        PYROXINITE_TYPE = dr["PYROXINITE_TYPE"].ToString(),
                        LIMESTONE_TYPE = dr["LIMESTONE_TYPE"].ToString()
                    }, JsonRequestBehavior.AllowGet);
                }
            }
        }
    }

    return Json(null, JsonRequestBehavior.AllowGet);
}