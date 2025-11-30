public ActionResult GetMaterials()
{
    List<string> materials = new List<string>();

    using (OracleConnection con = new OracleConnection("YOUR_CONN"))
    {
        con.Open();
        string query = "SELECT MATERIAL_NAME FROM T_MATERIAL_MASTER ORDER BY MATERIAL_NAME";

        using (OracleCommand cmd = new OracleCommand(query, con))
        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            while (dr.Read())
            {
                materials.Add(dr["MATERIAL_NAME"].ToString());
            }
        }
    }
    return Json(materials, JsonRequestBehavior.AllowGet);
}
