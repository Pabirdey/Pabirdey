[HttpPost]
public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
{
    RmbbPile model = new RmbbPile();
    ViewBag.Message = "";

    if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
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

                // If Save button is clicked
                if (!string.IsNullOrEmpty(SaveRawMaterial))
                {
                    if (count > 0)
                    {
                        // UPDATE
                        string updateSql = @"
                            UPDATE imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK SET
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
                            updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                            updateCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                            updateCmd.ExecuteNonQuery();
                            ViewBag.Message = "Record updated successfully.";
                        }
                    }
                    else
                    {
                        // INSERT
                        string insertSql = @"
                            INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                            (PILE_NO, SOURCE, PREP_START_DATE, PREP_END_DATE, CONS_ST_DATE, NOA_FINES, JODA_FINES, KB_FINES, YARD_FINES)
                            VALUES (:PILE_NO, :SOURCE, :PREP_START_DATE, :PREP_END_DATE, :CONS_ST_DATE, :NOA_FINES, :JODA_FINES, :KB_FINES, :YARD_FINES)";

                        using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                        {
                            insertCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                            insertCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;
                            insertCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;

                            insertCmd.ExecuteNonQuery();
                            ViewBag.Message = "New record inserted successfully.";
                        }
                    }

                    model = input; // Keep input values in form
                }
                else
                {
                    // No Save clicked — just check if data exists
                    if (count > 0)
                    {
                        string fetchSql = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
                        using (OracleCommand fetchCmd = new OracleCommand(fetchSql, conn))
                        {
                            fetchCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                            fetchCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                            using (OracleDataReader reader = fetchCmd.ExecuteReader())
                            {
                                if (reader.Read())
                                {
                                    model.PileNo = input.PileNo;
                                    model.Source = input.Source;
                                    model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? null : (DateTime?)reader["PREP_START_DATE"];
                                    model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? null : (DateTime?)reader["PREP_END_DATE"];
                                    model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? null : (DateTime?)reader["CONS_ST_DATE"];
                                    model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? null : (decimal?)reader["NOA_FINES"];
                                    model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? null : (decimal?)reader["JODA_FINES"];
                                    model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? null : (decimal?)reader["KB_FINES"];
                                    model.YARD_FINES = reader["YARD_FINES"] == DBNull.Value ? null : (decimal?)reader["YARD_FINES"];
                                }
                            }
                        }
                        ViewBag.Message = "Data loaded successfully.";
                    }
                    else
                    {
                        model = input;
                        ViewBag.Message = "No data found. Please fill and save.";
                    }
                }
            }
        }
    }

    return View(model);
}
