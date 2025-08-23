[HttpPost]
public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
{
    RmbbPile model = new RmbbPile();
    string message = "";

    // Validate required fields
    if (!string.IsNullOrEmpty(SaveRawMaterial))
    {
        if (string.IsNullOrEmpty(input.PileNo) || string.IsNullOrEmpty(input.Source))
        {
            ViewBag.Message = "PileNo and Source are required to save.";
            return View(input);
        }

        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            // Check if record exists
            string checkSql = "SELECT COUNT(*) FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
            using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
            {
                checkCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                checkCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                int count = Convert.ToInt32(checkCmd.ExecuteScalar());

                if (count > 0)
                {
                    // Perform UPDATE
                    string updateSql = @"UPDATE imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK SET
                                            PREP_START_DATE = :PREP_START_DATE,
                                            PREP_END_DATE = :PREP_END_DATE,
                                            CONS_ST_DATE = :CONS_ST_DATE,
                                            NOA_FINES = :NOA_FINES,
                                            JODA_FINES = :JODA_FINES,
                                            KB_FINES = :KB_FINES,
                                            YARD_FINES = :YARD_FINES
                                         WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";

                    using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                    {
                        updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                        updateCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                        updateCmd.ExecuteNonQuery();
                        message = "Record updated successfully.";
                    }
                }
                else
                {
                    // Perform INSERT
                    string insertSql = @"INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK
                        (PILE_NO, SOURCE, PREP_START_DATE, PREP_END_DATE, CONS_ST_DATE, NOA_FINES, JODA_FINES, KB_FINES, YARD_FINES)
                        VALUES (:PILE_NO, :SOURCE, :PREP_START_DATE, :PREP_END_DATE, :CONS_ST_DATE, :NOA_FINES, :JODA_FINES, :KB_FINES, :YARD_FINES)";

                    using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                    {
                        insertCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                        insertCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;
                        insertCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;

                        insertCmd.ExecuteNonQuery();
                        message = "Record inserted successfully.";
                    }
                }
            }
        }

        ViewBag.Message = message;
        model = input; // retain entered values
    }
    else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
        // Load existing data
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
            using (OracleCommand cmd = new OracleCommand(query, conn))
            {
                cmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                cmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        model.PileNo = input.PileNo;
                        model.Source = input.Source;
                        model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                        model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                        model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                        model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                        model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                        model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                        model.YARD_FINES = reader["YARD_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["YARD_FINES"]);
                    }
                }
            }
        }
    }

    return View(model);
}
