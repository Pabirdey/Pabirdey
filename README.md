public JsonResult GetData()
{
    List<object> list = new List<object>();

    using (OracleConnection con = new OracleConnection(conString))
    {
        con.Open();

        OracleCommand cmd = new OracleCommand("SELECT * FROM COKE_UNLOADING", con);

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            list.Add(new
            {
                TIMESTAMP = dr["TIMESTAMP"].ToString(),
                SHIFT = dr["SHIFT"].ToString(),
                BUNKER = dr["BUNKER"].ToString(),
                A = dr["A"].ToString(),
                B = dr["B"].ToString(),
                C = dr["C"].ToString(),
                D = dr["D"].ToString(),
                E = dr["E"].ToString(),
                F = dr["F"].ToString(),
                TOTAL = dr["TOTAL"].ToString(),
                BUNKER_P = dr["BUNKER_P"].ToString(),
                BALANCE = dr["BALANCE"].ToString()
            });
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}