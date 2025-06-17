public class Blast_FurnaceController : Controller
{
    string mycon = "User Id=...;Password=...;Data Source=..."; // your Oracle connection string

    [HttpGet]
    public ActionResult RawMaterial()
    {
        return View("RawMaterial_M", new RawMaterial_M());
    }

    [HttpPost]
    public ActionResult RawMaterial(RawMaterial_M model, string SaveRawMaterialM)
    {
        if (!string.IsNullOrEmpty(SaveRawMaterialM))
        {
            // Save logic
            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                {
                    cmd.CommandType = CommandType.StoredProcedure;

                    cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = model.PileNo ?? "";
                    cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = model.Source ?? "";
                    cmd.Parameters.Add("P_StartDate", OracleDbType.Date).Value = model.StartDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_EndDate", OracleDbType.Date).Value = model.EndDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_ConsStartDate", OracleDbType.Date).Value = model.ConsStartDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = model.NoaFines ?? 0;
                    cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
                    cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = model.KBFines ?? 0;
                    cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = model.YardFines ?? 0;

                    cmd.ExecuteNonQuery();
                }
            }

            ViewBag.Message = "Data Saved Successfully";
        }
        else if (!string.IsNullOrEmpty(model.PileNo) && !string.IsNullOrEmpty(model.Source))
        {
            // Load data on Source change
            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();
                string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO = :PileNo AND SOURCE = :Source";

                using (OracleCommand cmd = new OracleCommand(query, conn))
                {
                    cmd.Parameters.Add(new OracleParameter("PileNo", model.PileNo));
                    cmd.Parameters.Add(new OracleParameter("Source", model.Source));

                    using (OracleDataReader reader = cmd.ExecuteReader())
                    {
                        if (reader.Read())
                        {
                            model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                            model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                            model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                            model.NoaFines = reader["NOA_FINES"] == DBNull.Value ? 0 : Convert.ToDecimal(reader["NOA_FINES"]);
                            model.JodaFines = reader["JODA_FINES"] == DBNull.Value ? 0 : Convert.ToDecimal(reader["JODA_FINES"]);
                            model.KBFines = reader["KB_FINES"] == DBNull.Value ? 0 : Convert.ToDecimal(reader["KB_FINES"]);
                            model.YardFines = reader["YARD_FINES"] == DBNull.Value ? 0 : Convert.ToDecimal(reader["YARD_FINES"]);
                        }
                    }
                }
            }
        }

        return View("RawMaterial_M", model);
    }
}