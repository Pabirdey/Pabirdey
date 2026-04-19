public JsonResult SaveProductionData(BF_Production model)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // ================== COMMON MERGE QUERY ==================
            string mergeQuery = @"
MERGE INTO DEMO.T_BF_PRODUCTION_TRACKING t
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

            // ================== C, E, F LOOP ==================
            var furnaces = new[]
            {
                new { F="C", ACT=model.ACTUAL_C, REP=model.REPORTED_C, BAL=model.BALANCE_C, DT=model.DATE_TIME_PROD_C },
                new { F="E", ACT=model.ACTUAL_E, REP=model.REPORTED_E, BAL=model.BALANCE_E, DT=model.DATE_TIME_PROD_E },
                new { F="F", ACT=model.ACTUAL_F, REP=model.REPORTED_F, BAL=model.BALANCE_F, DT=model.DATE_TIME_PROD_F }
            };

            foreach (var f in furnaces)
            {
                using (OracleCommand cmd = new OracleCommand(mergeQuery, con))
                {
                    cmd.Parameters.Add("TIMESTAMP", f.DT);
                    cmd.Parameters.Add("FURNACE", f.F);
                    cmd.Parameters.Add("ACTUAL", f.ACT);
                    cmd.Parameters.Add("REPORTED", f.REP);
                    cmd.Parameters.Add("BALANCE", f.BAL);

                    cmd.ExecuteNonQuery();
                }
            }

            // ================== T_LADLE (A-F) ==================
            string ladleMerge = @"
MERGE INTO DEMO.T_LADLE t
USING (
    SELECT :DATE_TIME AS DATE_TIME, 'A-F' AS PLANT FROM dual
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
    INSERT (DATE_TIME, LD1_TONS, LD2_TONS, LD3_TONS, MRDTP_TONS, NOOFTP,
            LD1_TONS_ACTUAL, LD2_TONS_ACTUAL, LD3_TONS_ACTUAL, MRDTP_TONS_ACTUAL, PLANT)
    VALUES (:DATE_TIME, :LD1, :LD2, :LD3, :MRDTP, :NOOFTP,
            :LD1A, :LD2A, :LD3A, :MRDTPA, 'A-F')";

            using (OracleCommand cmd = new OracleCommand(ladleMerge, con))
            {
                cmd.Parameters.Add("DATE_TIME", model.DATE_TIME);
                cmd.Parameters.Add("LD1", model.LD1_TONS);
                cmd.Parameters.Add("LD2", model.LD2_TONS);
                cmd.Parameters.Add("LD3", model.LD3_TONS);
                cmd.Parameters.Add("MRDTP", model.MRDTP_TONS);
                cmd.Parameters.Add("NOOFTP", model.NOOFTP);

                cmd.Parameters.Add("LD1A", model.LD1_TONS_ACTUAL);
                cmd.Parameters.Add("LD2A", model.LD2_TONS_ACTUAL);
                cmd.Parameters.Add("LD3A", model.LD3_TONS_ACTUAL);
                cmd.Parameters.Add("MRDTPA", model.MRDTP_TONS_ACTUAL);

                cmd.ExecuteNonQuery();
            }

            // ================== TEST TABLE (ONLY C, E, F) ==================
            string testMerge = @"
MERGE INTO DEMO.T_BF_PRODUCTION_TEST t
USING (
    SELECT :TIMESTAMP AS TIMESTAMP, :FUR_NO AS FUR_NO FROM dual
) s
ON (t.TIMESTAMP = s.TIMESTAMP AND t.FUR_NO = s.FUR_NO)
WHEN MATCHED THEN
    UPDATE SET t.PRODUCTION = :PROD
WHEN NOT MATCHED THEN
    INSERT (TIMESTAMP, FUR_NO, PRODUCTION)
    VALUES (:TIMESTAMP, :FUR_NO, :PROD)";

            var testFurnaces = new[]
            {
                new { F=model.furnace_C, DT=model.DATE_TIME_PROD_C, PROD=model.REPORTED_C },
                new { F=model.furnace_E, DT=model.DATE_TIME_PROD_E, PROD=model.REPORTED_E },
                new { F=model.furnace_F, DT=model.DATE_TIME_PROD_F, PROD=model.REPORTED_F }
            };

            foreach (var f in testFurnaces)
            {
                using (OracleCommand cmd = new OracleCommand(testMerge, con))
                {
                    cmd.Parameters.Add("TIMESTAMP", f.DT);
                    cmd.Parameters.Add("FUR_NO", f.F);
                    cmd.Parameters.Add("PROD", f.PROD);

                    cmd.ExecuteNonQuery();
                }
            }
        }

        return Json(new { success = true, message = "Data Saved Successfully!" }, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}
