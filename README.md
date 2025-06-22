[HttpPost]
public ActionResult RawMaterialEntry(RawMaterialQuantity input)
{
    string message = "";
    using (OracleConnection conn = new OracleConnection(mycon))
    {
        conn.Open();

        // Check if the record already exists (for update)
        string checkSql = "SELECT COUNT(*) FROM RAW_MATERIAL_TABLE WHERE PILE_NO = :PileNo";
        using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
        {
            checkCmd.Parameters.Add("PileNo", OracleDbType.Varchar2).Value = input.PileNo;
            int count = Convert.ToInt32(checkCmd.ExecuteScalar());

            if (count > 0)
            {
                // Record exists -> UPDATE
                string updateSql = @"UPDATE RAW_MATERIAL_TABLE SET 
                                        SOURCE = :Source,
                                        END_DATE = :EndDate,
                                        CONST_START_DATE = :ConstStartDate,
                                        NOA_FINES = :NoaFines,
                                        JODA_FINES = :JodaFines
                                        -- Add more fields as needed
                                    WHERE PILE_NO = :PileNo";
                using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                {
                    updateCmd.Parameters.Add("Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                    updateCmd.Parameters.Add("EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                    updateCmd.Parameters.Add("ConstStartDate", OracleDbType.Date).Value = input.CONS_ST_DATE ?? (object)DBNull.Value;
                    updateCmd.Parameters.Add("NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? (object)DBNull.Value;
                    updateCmd.Parameters.Add("JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? (object)DBNull.Value;
                    updateCmd.Parameters.Add("PileNo", OracleDbType.Varchar2).Value = input.PileNo;

                    updateCmd.ExecuteNonQuery();
                    message = "Record updated successfully.";
                }
            }
            else
            {
                // Record does not exist -> INSERT
                string insertSql = @"INSERT INTO RAW_MATERIAL_TABLE 
                                     (PILE_NO, SOURCE, END_DATE, CONST_START_DATE, NOA_FINES, JODA_FINES) 
                                     VALUES 
                                     (:PileNo, :Source, :EndDate, :ConstStartDate, :NoaFines, :JodaFines)";
                using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                {
                    insertCmd.Parameters.Add("PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                    insertCmd.Parameters.Add("Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                    insertCmd.Parameters.Add("EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                    insertCmd.Parameters.Add("ConstStartDate", OracleDbType.Date).Value = input.CONS_ST_DATE ?? (object)DBNull.Value;
                    insertCmd.Parameters.Add("NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? (object)DBNull.Value;
                    insertCmd.Parameters.Add("JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? (object)DBNull.Value;

                    insertCmd.ExecuteNonQuery();
                    message = "Record inserted successfully.";
                }
            }
        }
    }

    ViewBag.Message = message;
    return View(input);
}