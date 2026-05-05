public JsonResult GetTonnageData(string date, string shift)
{
    List<object> cokeList = new List<object>();
    List<object> nutList = new List<object>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string query = @"
        SELECT BUNKER,
               TON_C_SC,TON_E_SC,TON_F_SC,
               TON_C_NC,TON_E_NC,TON_F_NC
        FROM imtg.T_BF_CK_CONTROL_UNLOADING 
        WHERE TRUNC(TIMESTAMP)=:date 
        AND SHIFT=:shift";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.BindByName = true;

            DateTime dt = DateTime.ParseExact(date, "dd/MM/yyyy", null);

            cmd.Parameters.Add("date", OracleDbType.Date).Value = dt;
            cmd.Parameters.Add("shift", OracleDbType.Varchar2).Value = shift;

            OracleDataReader dr = cmd.ExecuteReader();

            while (dr.Read())
            {
                // ✅ Coke (SC)
                cokeList.Add(new
                {
                    BUNKER = dr["BUNKER"].ToString(),
                    C = dr["TON_C_SC"].ToString(),
                    E = dr["TON_E_SC"].ToString(),
                    F = dr["TON_F_SC"].ToString()
                });

                // ✅ Nut (NC)
                nutList.Add(new
                {
                    BUNKER = dr["BUNKER"].ToString(),
                    C = dr["TON_C_NC"].ToString(),
                    E = dr["TON_E_NC"].ToString(),
                    F = dr["TON_F_NC"].ToString()
                });
            }
        }
    }

    return Json(new { coke = cokeList, nut = nutList }, JsonRequestBehavior.AllowGet);
}
