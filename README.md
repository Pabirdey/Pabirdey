public JsonResult GetTagValue(string tagId)
{
    string value = "";
    string timestamp = "";

    string constr = ConfigurationManager.ConnectionStrings["OracleDb"].ConnectionString;

    using (OracleConnection con = new OracleConnection(constr))
    {
        con.Open();

        string query = @"SELECT TIMESTAMP, VALUE 
                         FROM t_furnaces_proc_hm_prod 
                         WHERE TIMESTAMP = TO_DATE('24-FEB-2026','DD-MON-YYYY') 
                         AND TAG_ID = :tagId";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("tagId", tagId);

            OracleDataReader dr = cmd.ExecuteReader();
            if (dr.Read())
            {
                timestamp = dr["TIMESTAMP"].ToString();
                value = dr["VALUE"].ToString();
            }
        }
    }

    return Json(new { timestamp = timestamp, value = value }, JsonRequestBehavior.AllowGet);
}