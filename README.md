[HttpPost]
public ActionResult RawMaterialEntry(RawMaterialQuantity input)
{
    RawMaterialQuantity model = new RawMaterialQuantity
    {
        Source = input.Source,
        PileNo = input.PileNo
    };

    if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
        using (OracleConnection conn = new OracleConnection(mycon))
        {
            conn.Open();
            string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO = :PileNo AND SOURCE = :Source";
            using (OracleCommand cmd = new OracleCommand(query, conn))
            {
                cmd.Parameters.Add(new OracleParameter("PileNo", input.PileNo));
                cmd.Parameters.Add(new OracleParameter("Source", input.Source));
                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) : 0;
                        model.JodaFines = reader["JODA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["JODA_FINES"]) : 0;
                        model.KBFines = reader["KB_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["KB_FINES"]) : 0;
                        model.YardFines = reader["YARD_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["YARD_FINES"]) : 0;
                    }
                }
            }
        }
    }

    return View(model);
}