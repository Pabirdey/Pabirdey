  string query = @"MERGE INTO imtg.T_FURNACES_PROC_HM_PROD t
                                    USING (SELECT :TAG_ID TAG_ID FROM dual) s
                                    ON (t.TAG_ID = s.TAG_ID AND t.TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY'))
                                    WHEN MATCHED THEN
                                    UPDATE SET 
                                    t.VALUE = :VALUE_TON                                    
                                    WHEN NOT MATCHED THEN
                                    INSERT (TAG_ID,TIMESTAMP,VALUE)
                                    VALUES (:TAG_ID,TO_DATE(:FDate,'DD/MM/YYYY'),:VALUE_TON)";

                        foreach (var row in materials)
                        {
                            int tagId = Convert.ToInt32(row["TAG_ID"]);
                            decimal ton = Convert.ToDecimal(row["VALUE_TON"]);
                            using (OracleCommand cmd = new OracleCommand(query, con))
                            {
                                cmd.Transaction = trans;
                                cmd.BindByName = true;
                                cmd.Parameters.Add(":TAG_ID", OracleDbType.Int32).Value = tagId;
                                cmd.Parameters.Add(":FDate", OracleDbType.Varchar2).Value = FDate;
                                cmd.Parameters.Add(":VALUE_TON", OracleDbType.Decimal).Value = ton;
                                cmd.ExecuteNonQuery();
                            }
