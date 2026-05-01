        [HttpPost]
        public JsonResult Save_Furnace_High_Line(List<Furnace_High_line> list)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    using (OracleTransaction trans = con.BeginTransaction())
                    {
                        foreach (var item in list)
                        {
                            string sql = @"
                               MERGE INTO DEMO.T_HIGHLINE_REPORT_DATA t
                            USING (
                                SELECT :TAG_ID AS TAG_ID,                                                                            
                                       :val AS VALUE,
                                       :dt AS TIMESTAMP,
                                       :shift AS SHIFT
                                    FROM dual
                                  ) s
                                ON (t.TAG_ID = s.TAG_ID 
                                AND t.TIMESTAMP = s.TIMESTAMP 
                                AND t.SHIFT = s.SHIFT)
                                WHEN MATCHED THEN
                                    UPDATE SET 
                                        t.TAG_VAL = s.val                                                                              
                                WHEN NOT MATCHED THEN
                                    INSERT (TIMESTAMP,SHIFT,TAG_ID,TAG_VAL)
                                    VALUES (s.dt,s.shift,s.TAG_ID,s.val)";

                            using (OracleCommand cmd = new OracleCommand(sql, con))
                            {
                                cmd.Transaction = trans;
                                cmd.Parameters.Add(":TAG_ID", OracleDbType.Int32).Value = item.CellId;                                                             
                                cmd.Parameters.Add(":val", OracleDbType.Decimal).Value = (object)item.Value ?? DBNull.Value;
                                cmd.Parameters.Add(":dt", OracleDbType.Date).Value = item.Date;
                                cmd.Parameters.Add(":shift", OracleDbType.Varchar2).Value = item.Shift;
                                cmd.ExecuteNonQuery();
                            }
                        }

                        trans.Commit();
                    }
                }

                return Json(new { success = true });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
