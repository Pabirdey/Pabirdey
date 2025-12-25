[HttpGet]
public ActionResult GetRawMaterialByFurnace(string furnace, string fdate)
{
    var list = new List<object>();

    using (var conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();

        using (var cmd = new OracleCommand("PROC_GET_RAW_MATERIAL", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;

            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;

            // Convert string date to Date
            cmd.Parameters.Add("p_date", OracleDbType.Date)
                          .Value = Convert.ToDateTime(fdate);

            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor)
                          .Direction = ParameterDirection.Output;

            using (var dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(new
                    {
                        MATERIAL = dr["MATERIAL_NAME"],
                        VALUE_TON = dr["VALUE_TON"],
                        VALUE_KG = dr["VALUE_KG"]
                    });
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}