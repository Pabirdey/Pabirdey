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
                // =========================
                // 1. TABLE 1: TRACKING
                // =========================
                string query1 = @"
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

                using (OracleCommand cmd = new OracleCommand(query1, con))
                {
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                    cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = Convert.ToDateTime(model.DATE_TIME);
                    cmd.Parameters.Add("ACT", OracleDbType.Decimal).Value = model.ACT_ONDT;
                    cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;
                    cmd.Parameters.Add("BAL", OracleDbType.Decimal).Value = model.BALANCE;

                    cmd.ExecuteNonQuery();
                }

                // =========================
                // 2. TABLE 2: TEST TABLE
                // =========================
                string query2 = @"
MERGE INTO TEST.T_BF_PRODUCTION_TEST t
USING (
    SELECT :FURNACE AS FURNACE,
           :DATE_TIME AS TIMESTAMP
    FROM dual
) s
ON (t.FUR_NO = s.FURNACE AND t.TIMESTAMP = s.TIMESTAMP)

WHEN MATCHED THEN
    UPDATE SET 
        PRODUCTION = :RPT

WHEN NOT MATCHED THEN
    INSERT (FUR_NO, TIMESTAMP, PRODUCTION)
    VALUES (:FURNACE, :DATE_TIME, :RPT)";

                using (OracleCommand cmd = new OracleCommand(query2, con))
                {
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                    cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = Convert.ToDateTime(model.DATE_TIME);
                    cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;

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