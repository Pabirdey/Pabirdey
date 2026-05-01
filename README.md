[HttpPost]
        public JsonResult SaveData(List<CellData> list)
        {
            try
            {

                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    using (OracleTransaction rans = con.BeginTransaction())
                    {
                        foreach (var item in list)
                        {
                            string sql = @"
                        MERGE INTO RAW_MATERIAL_TABLE t
                        USING (
                            SELECT :cellid AS CELL_ID,
                                   :mat AS MATERIAL,
                                   :pos AS POSITION,
                                   :val AS VALUE,
                                   TO_DATE(:dt,'YYYY-MM-DD') AS ENTRY_DATE,
                                   :shift AS SHIFT
                            FROM dual
                        ) s
                        ON (t.CELL_ID = s.CELL_ID 
                            AND t.ENTRY_DATE = s.ENTRY_DATE 
                            AND t.SHIFT = s.SHIFT)

                        WHEN MATCHED THEN
                            UPDATE SET 
                                t.MATERIAL = s.MATERIAL,
                                t.POSITION = s.POSITION,
                                t.VALUE = s.VALUE

                        WHEN NOT MATCHED THEN
                            INSERT (CELL_ID, MATERIAL, POSITION, VALUE, ENTRY_DATE, SHIFT)
                            VALUES (s.CELL_ID, s.MATERIAL, s.POSITION, s.VALUE, s.ENTRY_DATE, s.SHIFT)";

                            using (OracleCommand cmd = new OracleCommand(sql, con))
                            {
                                cmd.Transaction = trans;
                                cmd.Parameters.Add(":cellid", item.CellId);
                                cmd.Parameters.Add(":mat", item.Material);
                                cmd.Parameters.Add(":pos", item.Position);
                                cmd.Parameters.Add(":val", item.Value ?? (object)DBNull.Value);
                                cmd.Parameters.Add(":dt", item.Date);
                                cmd.Parameters.Add(":shift", item.Shift);

                                cmd.ExecuteNonQuery();
                            }
                        }

                        trans.Commit(); // ✅ commit once (faster)
                    }
                }

                return Json(new { success = true });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
