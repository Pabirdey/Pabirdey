public ActionResult GetRawMaterialByFurnace(string furnace, string fdate)
{
    var list = new List<RawMaterialModel>();

    using (OracleConnection conn = new OracleConnection("Your Connection"))
    {
        conn.Open();

        using (OracleCommand cmd = new OracleCommand("PROC_GET_RAW_MATERIAL", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;

            cmd.Parameters.Add("p_furnace", furnace);
            cmd.Parameters.Add("p_date", fdate);
            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor).Direction = ParameterDirection.Output;

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(new RawMaterialModel
                    {
                        Material = dr["MATERIAL_NAME"].ToString(),
                        ValueTon = dr["VALUE_TON"].ToString(),
                        ValueKg = dr["VALUE_KG"].ToString(),
                        TypeName = dr["TYPE_NAME"].ToString()
                    });
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}