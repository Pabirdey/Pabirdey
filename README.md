[HttpPost]
public JsonResult SaveBFRawMaterialData(
        string REPORT_DATE,
        string FURNACE,
        List<Dictionary<string, object>> materials)
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
                string query = @"
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
                        VALUES (:TAG_ID,
                                TO_DATE(:REPORT_DATE,'YYYY-MM-DD'),
                                :FURNACE,
                                :VALUE_TON,
                                :VALUE_KG)";

                foreach (var row in materials)
                {
                    int tagId = Convert.ToInt32(row["TAG_ID"]);
                    decimal ton = Convert.ToDecimal(row["VALUE_TON"]);
                    decimal kg = Convert.ToDecimal(row["VALUE_KG"]);

                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        cmd.Transaction = trans;
                        cmd.BindByName = true;   // 🔥 Important in Oracle

                        cmd.Parameters.Add(":TAG_ID", OracleDbType.Int32).Value = tagId;
                        cmd.Parameters.Add(":REPORT_DATE", OracleDbType.Varchar2).Value = REPORT_DATE;
                        cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = FURNACE;
                        cmd.Parameters.Add(":VALUE_TON", OracleDbType.Decimal).Value = ton;
                        cmd.Parameters.Add(":VALUE_KG", OracleDbType.Decimal).Value = kg;

                        cmd.ExecuteNonQuery();
                    }
                }

                trans.Commit();

                return Json(new
                {
                    status = true,
                    message = "All Data Saved Successfully"
                });
            }
            catch (Exception ex)
            {
                trans.Rollback();

                return Json(new
                {
                    status = false,
                    message = ex.Message
                });
            }
        }
    }
}
