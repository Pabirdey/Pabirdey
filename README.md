public JsonResult SaveBFProduction(BFProductionSaveModel model)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            using (OracleTransaction trans = con.BeginTransaction())
            {
                try
                {
                    // ==============================
                    // 1. SAVE BF_PRODUCTION_TRACKING
                    // ==============================
                    foreach (var f in model.Furnaces)
                    {
                        string mergeQuery = @"
MERGE INTO TEST.T_BF_PRODUCTION_TRACKING t
USING (
    SELECT :TIMESTAMP AS TIMESTAMP, :FURNACE AS FURNACE FROM dual
) s
ON (t.TIMESTAMP = s.TIMESTAMP AND t.FURNACE = s.FURNACE)
WHEN MATCHED THEN
    UPDATE SET 
        t.ACTUAL = :ACTUAL,
        t.REPORTED = :REPORTED,
        t.BALANCE = :BALANCE
WHEN NOT MATCHED THEN
    INSERT (TIMESTAMP, FURNACE, ACTUAL, REPORTED, BALANCE)
    VALUES (:TIMESTAMP, :FURNACE, :ACTUAL, :REPORTED, :BALANCE)";

                        using (OracleCommand cmd = new OracleCommand(mergeQuery, con))
                        {
                            cmd.Transaction = trans;
                            cmd.BindByName = true;

                            cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = model.DateTime;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = f.Furnace;
                            cmd.Parameters.Add("ACTUAL", OracleDbType.Decimal).Value = f.Actual;
                            cmd.Parameters.Add("REPORTED", OracleDbType.Decimal).Value = f.Reported;
                            cmd.Parameters.Add("BALANCE", OracleDbType.Decimal).Value = f.Balance;

                            cmd.ExecuteNonQuery();
                        }

                        // ==============================
                        // 2. SAVE TEST TABLE
                        // ==============================
                        string testMerge = @"
MERGE INTO TEST.T_BF_PRODUCTION_TEST t
USING (
    SELECT :TIMESTAMP AS TIMESTAMP, :FURNACE AS FURNACE FROM dual
) s
ON (t.TIMESTAMP = s.TIMESTAMP AND t.FUR_NO = s.FURNACE)
WHEN MATCHED THEN
    UPDATE SET t.PRODUCTION = :REPORTED
WHEN NOT MATCHED THEN
    INSERT (TIMESTAMP, FUR_NO, PRODUCTION)
    VALUES (:TIMESTAMP, :FURNACE, :REPORTED)";

                        using (OracleCommand cmd = new OracleCommand(testMerge, con))
                        {
                            cmd.Transaction = trans;
                            cmd.BindByName = true;

                            cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = model.DateTime;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = f.Furnace;
                            cmd.Parameters.Add("REPORTED", OracleDbType.Decimal).Value = f.Reported;

                            cmd.ExecuteNonQuery();
                        }
                    }

                    // ==============================
                    // 3. SAVE LADLE TABLE
                    // ==============================
                    string ladleMerge = @"
MERGE INTO TEST.T_LADLE t
USING (
    SELECT :DATE_TIME AS DATE_TIME, :PLANT AS PLANT FROM dual
) s
ON (t.DATE_TIME = s.DATE_TIME AND t.PLANT = s.PLANT)
WHEN MATCHED THEN
    UPDATE SET 
        t.LD1_TONS = :LD1,
        t.LD2_TONS = :LD2,
        t.LD3_TONS = :LD3,
        t.MRDTP_TONS = :MRDTP,
        t.NOOFTP = :NOOFTP
WHEN NOT MATCHED THEN
    INSERT (DATE_TIME, LD1_TONS, LD2_TONS, LD3_TONS, MRDTP_TONS, NOOFTP, PLANT)
    VALUES (:DATE_TIME, :LD1, :LD2, :LD3, :MRDTP, :NOOFTP, :PLANT)";

                    using (OracleCommand cmd = new OracleCommand(ladleMerge, con))
                    {
                        cmd.Transaction = trans;
                        cmd.BindByName = true;

                        cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = model.DateTime;
                        cmd.Parameters.Add("PLANT", OracleDbType.Varchar2).Value = model.Plant;

                        cmd.Parameters.Add("LD1", OracleDbType.Decimal).Value = model.LD1_TONS;
                        cmd.Parameters.Add("LD2", OracleDbType.Decimal).Value = model.LD2_TONS;
                        cmd.Parameters.Add("LD3", OracleDbType.Decimal).Value = model.LD3_TONS;
                        cmd.Parameters.Add("MRDTP", OracleDbType.Decimal).Value = model.MRDTP_TONS;
                        cmd.Parameters.Add("NOOFTP", OracleDbType.Decimal).Value = model.NOOFTP;

                        cmd.ExecuteNonQuery();
                    }

                    trans.Commit();

                    return Json(new { success = true, message = "Saved Successfully" });
                }
                catch (Exception ex)
                {
                    trans.Rollback();
                    return Json(new { success = false, message = ex.Message });
                }
            }
        }
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message });
    }
}
