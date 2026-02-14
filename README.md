[HttpPost]
        public JsonResult SaveBFRawMaterialData(string FDate, string furnace, List<Dictionary<string, object>> materials)
        {
            if (materials == null || materials.Count == 0)
                return Json(new { status = false, message = "No data received." });

            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                using (OracleTransaction trans = con.BeginTransaction())
                {
                    try
                    {
                        string query = @"MERGE INTO TEST.T_FURNACES_PROC_HM_PROD t
                                    USING (SELECT :TAG_ID TAG_ID FROM dual) s
                                    ON (t.TAG_ID = s.TAG_ID AND t.TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY'))
                                    WHEN MATCHED THEN
                                    UPDATE SET 
                                    t.VALUE = :VALUE                                    
                                    WHEN NOT MATCHED THEN
                                    INSERT (TAG_ID,TIMESTAMP,VALUE)
                                    VALUES (:TAG_ID,TO_DATE(:FDate,'DD/MM/YYYY'),:VALUE)";

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
                                cmd.Parameters.Add(":VALUE", OracleDbType.Decimal).Value = ton;                             
                                cmd.ExecuteNonQuery();
                            }
                        }

                        trans.Commit();
                        return Json(new{status = true,message = "All Data Saved Successfully"});
                    }
                    catch (Exception ex)
                    {
                        trans.Rollback();
                        return Json(new{status = false,message = ex.Message});
                    }
                }
            }
        }
