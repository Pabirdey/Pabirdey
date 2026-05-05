public JsonResult GetTonnageData(string date, string shift)
{
    List<object> cokeList = new List<object>();
    List<object> nutList = new List<object>();

    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string query = @"
            SELECT BUNKER,
                   TON_C_SC,TON_E_SC,TON_F_SC,
                   TON_C_NC,TON_E_NC,TON_F_NC
            FROM imtg.T_BF_CK_CONTROL_UNLOADING 
            WHERE TRUNC(""TIMESTAMP"") = :p_date 
            AND SHIFT = :p_shift";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.BindByName = true;

                DateTime dt = DateTime.ParseExact(date, "dd/MM/yyyy", null);

                cmd.Parameters.Add("p_date", OracleDbType.Date).Value = dt;
                cmd.Parameters.Add("p_shift", OracleDbType.Varchar2).Value = shift;

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        cokeList.Add(new
                        {
                            BUNKER = dr["BUNKER"].ToString(),
                            C = dr["TON_C_SC"].ToString(),
                            E = dr["TON_E_SC"].ToString(),
                            F = dr["TON_F_SC"].ToString()
                        });

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
        }

        return Json(new { success = true, coke = cokeList, nut = nutList }, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}
