  [HttpPost]
        public JsonResult SaveBFRawMaterialData(List<Dictionary<string, object>> data)
        {           

            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                using (OracleTransaction trans = con.BeginTransaction())
                {
                    try
                    {
                        foreach (var row in data)
                        {
                            string reportDate = row["REPORT_DATE"].ToString();
                            string furnace = row["FURNACE"].ToString();
                            int tagId = Convert.ToInt32(row["TAG_ID"]);
                            decimal ton = Convert.ToDecimal(row["VALUE_TON"]);
                            decimal kg = Convert.ToDecimal(row["VALUE_KG"]);

                            using (OracleCommand cmd = new OracleCommand(@"
                        MERGE INTO T_RAW_MATERIAL t
                        USING (SELECT :TAG_ID TAG_ID FROM dual) s
                        ON (t.TAG_ID = s.TAG_ID
                            AND t.REPORT_DATE = TO_DATE(:REPORT_DATE,'YYYY-MM-DD')
                            AND t.FURNACE = :FURNACE)
                        WHEN MATCHED THEN
                            UPDATE SET 
                                t.VALUE_TON = :VALUE_TON,
                                t.VALUE_KG = :VALUE_KG
                        WHEN NOT MATCHED THEN
                            INSERT (TAG_ID, REPORT_DATE, FURNACE, VALUE_TON, VALUE_KG)
                            VALUES (:TAG_ID, TO_DATE(:REPORT_DATE,'YYYY-MM-DD'),
                                    :FURNACE, :VALUE_TON, :VALUE_KG)
                    ", con))
                            {
                                cmd.Transaction = trans;

                                cmd.Parameters.Add(":TAG_ID", OracleDbType.Int32).Value = tagId;
                                cmd.Parameters.Add(":REPORT_DATE", OracleDbType.Varchar2).Value = reportDate;
                                cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = furnace;
                                cmd.Parameters.Add(":VALUE_TON", OracleDbType.Decimal).Value = ton;
                                cmd.Parameters.Add(":VALUE_KG", OracleDbType.Decimal).Value = kg;

                                cmd.ExecuteNonQuery();
                            }
                        }

                        trans.Commit();  
                        return Json(new { message = "All Data Saved Successfully" });
                    }
                    catch (Exception ex)
                    {
                        trans.Rollback();
                        return Json(new { message = "Error: " + ex.Message });
                    }
                }
            }
        }
