[HttpPost]
public JsonResult SaveCBFBulk(List<BF_Production> modelList)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            foreach (var model in modelList)
            {
                string query = @"
                MERGE INTO DEMO.T_BF_PRODUCTION_TRACKING t
                USING (SELECT :FURNACE AS FURNACE FROM dual) s
                ON (t.FURNACE = s.FURNACE)
                WHEN MATCHED THEN
                    UPDATE SET 
                        ACTUAL = :ACT,
                        REPORTED = :RPT,
                        BALANCE = :BAL
                WHEN NOT MATCHED THEN
                    INSERT (FURNACE, ACTUAL, REPORTED, BALANCE)
                    VALUES (:FURNACE, :ACT, :RPT, :BAL)";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("FURNACE", model.FURNACE_C);
                    cmd.Parameters.Add("ACT", model.ACT_ONDT);
                    cmd.Parameters.Add("RPT", model.REPORT_ONDT);
                    cmd.Parameters.Add("BAL", model.BALANCE);

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
