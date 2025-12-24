[HttpGet]
public ActionResult GetRawMaterialByFurnace(string furnace, string fdate)
{
    var list = new List<Dictionary<string, object>>();

    using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();

        using (OracleCommand cmd = new OracleCommand("PROC_GET_RAW_MATERIAL", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;
            cmd.BindByName = true;

            // 🔹 Param 1 - Furnace
            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;

            // 🔹 Param 2 - Date (Convert to Oracle DATE)
            DateTime dt = DateTime.ParseExact(fdate, "dd/MM/yyyy",
                                  System.Globalization.CultureInfo.InvariantCulture);
            cmd.Parameters.Add("p_date", OracleDbType.Date).Value = dt;

            // 🔹 Param 3 - Ref Cursor OUT
            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor).Direction = ParameterDirection.Output;

            // 🔹 Execute
            cmd.ExecuteNonQuery();

            // 🔹 Read Cursor Data
            OracleDataReader dr = ((OracleRefCursor)cmd.Parameters["p_cursor"].Value).GetDataReader();

            while (dr.Read())
            {
                var row = new Dictionary<string, object>();

                row["MATERIAL"] = dr["MATERIAL_NAME"].ToString();
                row["VALUE_TON"] = dr["VALUE_TON"].ToString();
                row["VALUE_KG"] = dr["VALUE_KG"].ToString();

                list.Add(row);
            }

            dr.Close();
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}