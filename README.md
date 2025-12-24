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

            // Furnace
            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;

            // Safely handle date
            DateTime dt;
            if (!DateTime.TryParseExact(fdate, "dd/MM/yyyy",
                System.Globalization.CultureInfo.InvariantCulture,
                System.Globalization.DateTimeStyles.None,
                out dt))
            {
                return Json(new { error = "Invalid date format. Use dd/MM/yyyy" }, JsonRequestBehavior.AllowGet);
            }

            cmd.Parameters.Add("p_date", OracleDbType.Date).Value = dt;

            // Ref Cursor
            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor).Direction = ParameterDirection.Output;

            cmd.ExecuteNonQuery();

            using (OracleDataReader dr = ((OracleRefCursor)cmd.Parameters["p_cursor"].Value).GetDataReader())
            {
                while (dr.Read())
                {
                    var row = new Dictionary<string, object>();

                    row["MATERIAL"] = dr["MATERIAL_NAME"]?.ToString();
                    row["VALUE_TON"] = dr["VALUE_TON"]?.ToString();
                    row["VALUE_KG"] = dr["VALUE_KG"]?.ToString();

                    list.Add(row);
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}