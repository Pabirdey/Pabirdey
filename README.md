[HttpPost]
public JsonResult SaveBFProdData(List<BF_Production> modelList)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            foreach (var model in modelList)
            {
                string query = @"
MERGE INTO TEST.T_BF_PRODUCTION_TRACKING t
USING (
    SELECT :FURNACE AS FURNACE,
           :DATE_TIME AS TIMESTAMP
    FROM dual
) s
ON (t.FURNACE = s.FURNACE AND t.TIMESTAMP = s.TIMESTAMP)

WHEN MATCHED THEN
    UPDATE SET 
        ACTUAL = :ACT,
        REPORTED = :RPT,
        BALANCE = :BAL

WHEN NOT MATCHED THEN
    INSERT (FURNACE, TIMESTAMP, ACTUAL, REPORTED, BALANCE)
    VALUES (:FURNACE, :DATE_TIME, :ACT, :RPT, :BAL)";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;

                    // 🔥 FIXED DATE HANDLING (NO TO_DATE)
                    cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value =
                        Convert.ToDateTime(model.DATE_TIME);

                    cmd.Parameters.Add("ACT", OracleDbType.Decimal).Value = model.ACT_ONDT;
                    cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;
                    cmd.Parameters.Add("BAL", OracleDbType.Decimal).Value = model.BALANCE;

                    cmd.ExecuteNonQuery();
                }
            }
        }

        return Json(new { success = true });
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message });
    }
}
