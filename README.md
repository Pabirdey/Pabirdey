[HttpPost]
public JsonResult SaveCarbonPasteData(string jsonData, string date, string source)
{
    try
    {
        var dataList = Newtonsoft.Json.JsonConvert.DeserializeObject<List<dynamic>>(jsonData);

        string connectionString = "User Id=your_user;Password=your_password;Data Source=your_datasource";

        using (OracleConnection conn = new OracleConnection(connectionString))
        {
            conn.Open();

            foreach (var row in dataList)
            {
                string dateTime = row.DateTime.ToString();
                string shift = row.Shift.ToString();
                string belowTuyere = row.BelowTuyere.ToString();
                string noOfDrum = row.NoOfDrum.ToString();

                // Sample upsert logic, you can modify it to use 'date' and 'source' if required
                string checkSql = @"SELECT COUNT(*) FROM CARBON_PASTE_INJ 
                                    WHERE DATETIME = TO_DATE(:DateTime, 'YYYY-MM-DD HH24:MI:SS') 
                                    AND SHIFT = :Shift
                                    AND SOURCE = :Source
                                    AND ENTRY_DATE = TO_DATE(:EntryDate, 'YYYY-MM-DD')";

                using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
                {
                    checkCmd.Parameters.Add(":DateTime", dateTime);
                    checkCmd.Parameters.Add(":Shift", shift);
                    checkCmd.Parameters.Add(":Source", source);
                    checkCmd.Parameters.Add(":EntryDate", date);

                    int count = Convert.ToInt32(checkCmd.ExecuteScalar());

                    if (count > 0)
                    {
                        string updateSql = @"UPDATE CARBON_PASTE_INJ SET 
                                                BELOW_TUYERE = :BelowTuyere,
                                                NO_OF_DRUM = :NoOfDrum
                                             WHERE 
                                                DATETIME = TO_DATE(:DateTime, 'YYYY-MM-DD HH24:MI:SS') 
                                                AND SHIFT = :Shift
                                                AND SOURCE = :Source
                                                AND ENTRY_DATE = TO_DATE(:EntryDate, 'YYYY-MM-DD')";

                        using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                        {
                            updateCmd.Parameters.Add(":BelowTuyere", belowTuyere);
                            updateCmd.Parameters.Add(":NoOfDrum", noOfDrum);
                            updateCmd.Parameters.Add(":DateTime", dateTime);
                            updateCmd.Parameters.Add(":Shift", shift);
                            updateCmd.Parameters.Add(":Source", source);
                            updateCmd.Parameters.Add(":EntryDate", date);

                            updateCmd.ExecuteNonQuery();
                        }
                    }
                    else
                    {
                        string insertSql = @"INSERT INTO CARBON_PASTE_INJ (
                                                DATETIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM, SOURCE, ENTRY_DATE
                                             ) VALUES (
                                                TO_DATE(:DateTime, 'YYYY-MM-DD HH24:MI:SS'),
                                                :Shift, :BelowTuyere, :NoOfDrum, :Source, TO_DATE(:EntryDate, 'YYYY-MM-DD')
                                             )";

                        using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                        {
                            insertCmd.Parameters.Add(":DateTime", dateTime);
                            insertCmd.Parameters.Add(":Shift", shift);
                            insertCmd.Parameters.Add(":BelowTuyere", belowTuyere);
                            insertCmd.Parameters.Add(":NoOfDrum", noOfDrum);
                            insertCmd.Parameters.Add(":Source", source);
                            insertCmd.Parameters.Add(":EntryDate", date);

                            insertCmd.ExecuteNonQuery();
                        }
                    }
                }
            }

            conn.Close();
        }

        return Json(new { success = true });
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message });
    }
}
