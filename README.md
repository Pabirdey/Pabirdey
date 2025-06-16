[HttpPost]
public ActionResult SaveRawMaterial(RawMaterialQuantity model)
{
    string conString = ConfigurationManager.ConnectionStrings["OracleDbContext"].ConnectionString;

    using (OracleConnection conn = new OracleConnection(conString))
    {
        conn.Open();

        using (OracleCommand cmd = new OracleCommand("SAVE_RAW_MATERIAL_QTY", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;

            // Required header fields
            cmd.Parameters.Add("P_PILE_NO", OracleDbType.Varchar2).Value = model.PileNo ?? "";
            cmd.Parameters.Add("P_SOURCE", OracleDbType.Varchar2).Value = model.Source ?? "";
            cmd.Parameters.Add("P_SHIFT", OracleDbType.Varchar2).Value = model.Shift ?? "";
            cmd.Parameters.Add("P_START_DATE", OracleDbType.Date).Value = model.StartDate ?? (object)DBNull.Value;
            cmd.Parameters.Add("P_END_DATE", OracleDbType.Date).Value = model.EndDate ?? (object)DBNull.Value;
            cmd.Parameters.Add("P_CONS_SL_DATE", OracleDbType.Date).Value = model.ConsSlDate ?? (object)DBNull.Value;

            // Sample material entries (only a few — add all as required)
            cmd.Parameters.Add("P_JODA_FINES", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
            cmd.Parameters.Add("P_KB_FINES", OracleDbType.Decimal).Value = model.KbFines ?? 0;
            cmd.Parameters.Add("P_SOLID_WASTE", OracleDbType.Decimal).Value = model.SolidWaste ?? 0;
            // Add all 40+ other material fields like above...

            cmd.ExecuteNonQuery();
        }
    }

    TempData["Success"] = "Data saved successfully!";
    return RedirectToAction("RawMaterialEntry"); // or your view
}