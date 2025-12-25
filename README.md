[HttpGet]
public ActionResult GetRawMaterialByFurnace(string furnace, string fdate)
{
    var list = new List<Dictionary<string, object>>();

    using (var conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();

        using (var cmd = new OracleCommand("PROC_GET_RAW_MATERIAL", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;
            cmd.BindByName = true;

            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;
            cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = fdate;
            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor).Direction = ParameterDirection.Output;

            var da = new OracleDataAdapter(cmd);
            var dt = new DataTable();
            da.Fill(dt);

            foreach (DataRow dr in dt.Rows)
            {
                var row = new Dictionary<string, object>();

                row["MATERIAL"] = dr["MATERIAL_NAME"]?.ToString();
                row["VALUE_TON"] = dr["VALUE_TON"]?.ToString();
                row["VALUE_KG"] = dr["VALUE_KG"]?.ToString();

                list.Add(row);
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}