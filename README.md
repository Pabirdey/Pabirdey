public ActionResult GetMaterials(string furnace)
{
    List<string> list = new List<string>();

    using (OracleConnection con = new OracleConnection("YOUR_CONN"))
    {
        con.Open();

        string q = @"SELECT MATERIAL_NAME 
                     FROM T_MATERIAL_MASTER 
                     WHERE FURNACE = :FURNACE 
                     ORDER BY MATERIAL_NAME";

        using (OracleCommand cmd = new OracleCommand(q, con))
        {
            cmd.Parameters.Add(":FURNACE", furnace);

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(dr["MATERIAL_NAME"].ToString());
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
