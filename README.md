public JsonResult GetClayList()
{
    List<string> list = new List<string>();

    using (OracleConnection con = new OracleConnection(ConfigurationManager.ConnectionStrings["ConStr"].ConnectionString))
    {
        con.Open();
        string query = "SELECT CLAY_NAME FROM MG_CLAY_MASTER ORDER BY CLAY_NAME";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(dr["CLAY_NAME"].ToString());
                }
            }
        }
    }
    return Json(list, JsonRequestBehavior.AllowGet);
}