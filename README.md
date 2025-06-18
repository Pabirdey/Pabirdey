[HttpPost]
public ActionResult RawMaterialEntry(RawMaterialQuantity input, string SaveRawMaterial)
{
    if (!string.IsNullOrEmpty(SaveRawMaterial))
    {
        using (OracleConnection conn = new OracleConnection(mycon))
        {
            conn.Open();

            using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
            {
                cmd.CommandType = CommandType.StoredProcedure;

                // Assigning input values directly (not a partial new object)
                cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? 0;
                cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? 0;
                cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = input.KBFines ?? 0;
                cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = input.YardFines ?? 0;

                cmd.ExecuteNonQuery();
            }
        }

        ViewBag.Message = "Data Saved Successfully";
    }

    return View("RawMaterialEntry", input);  // Return same view with current data
}