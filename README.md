[HttpPost]
public ActionResult SaveMultipleRawMaterials(RawMaterialQuantityViewModel viewModel)
{
    string conStr = ConfigurationManager.ConnectionStrings["OracleDbContext"].ConnectionString;

    using (OracleConnection conn = new OracleConnection(conStr))
    {
        conn.Open();

        foreach (var item in viewModel.Items)
        {
            using (OracleCommand cmd = new OracleCommand("YOUR_PACKAGE.SAVE_OR_UPDATE_RAWMAT", conn))
            {
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add("P_PILENO", OracleDbType.Varchar2).Value = item.PileNo;
                cmd.Parameters.Add("P_SOURCE", OracleDbType.Varchar2).Value = item.Source;
                cmd.Parameters.Add("P_QTY1", OracleDbType.Decimal).Value = item.Quantity1;
                cmd.Parameters.Add("P_QTY2", OracleDbType.Decimal).Value = item.Quantity2;
                cmd.Parameters.Add("P_QTY3", OracleDbType.Decimal).Value = item.Quantity3;

                cmd.Parameters.Add("P_STATUS", OracleDbType.Varchar2, 200).Direction = ParameterDirection.Output;

                cmd.ExecuteNonQuery();
                string status = cmd.Parameters["P_STATUS"].Value.ToString();
                // Optionally: log or collect status
            }
        }
    }

    ViewBag.Message = "All rows saved/updated successfully.";
    return View("RawMaterialForm", viewModel); // or RedirectToAction("Index")
}