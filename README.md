public JsonResult GetUsers()
{
    List<object> list = new List<object>();

    using (OracleConnection con =
        new OracleConnection("YOUR_CONNECTION_STRING"))
    {
        con.Open();

        string query = @"SELECT USER_NAME
                         FROM USER_MASTER
                         ORDER BY USER_NAME";

        OracleCommand cmd = new OracleCommand(query, con);

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            list.Add(new
            {
                USER_NAME = dr["USER_NAME"].ToString()
            });
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
