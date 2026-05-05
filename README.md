[HttpPost]
public JsonResult SaveData(SaveModel model)
{
    using (OracleConnection con = new OracleConnection("YOUR_CONNECTION"))
    {
        con.Open();
        OracleTransaction trans = con.BeginTransaction();

        try
        {
            // ============================
            // 🔷 MAIN DATA
            // ============================
            foreach (var item in model.main)
            {
                string query = @"
                MERGE INTO T_COKE_ALL t
                USING dual
                ON (t.TDATE = TO_DATE(:TDATE,'DD/MM/YYYY') 
                    AND t.SHIFT = :SHIFT 
                    AND t.BUNKER = :BUNKER
                    AND t.CATEGORY = 'MAIN')

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL,
                        t.POSITION = :POSITION,
                        t.BALANCE = :BALANCE

                WHEN NOT MATCHED THEN
                    INSERT (TDATE, SHIFT, BUNKER, C_BF, E_BF, F_BF, TOTAL, POSITION, BALANCE, CATEGORY)
                    VALUES (TO_DATE(:TDATE,'DD/MM/YYYY'), :SHIFT, :BUNKER, :C, :E, :F, :TOTAL, :POSITION, :BALANCE, 'MAIN')";
                
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("TDATE", item.Date);
                    cmd.Parameters.Add("SHIFT", item.Shift);
                    cmd.Parameters.Add("BUNKER", item.Bunker);

                    cmd.Parameters.Add("C", item.C ?? "0");
                    cmd.Parameters.Add("E", item.E ?? "0");
                    cmd.Parameters.Add("F", item.F ?? "0");
                    cmd.Parameters.Add("TOTAL", item.Total ?? "0");

                    cmd.Parameters.Add("POSITION", item.Position ?? "0");
                    cmd.Parameters.Add("BALANCE", item.Balance ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            // ============================
            // 🔷 COKE DATA
            // ============================
            foreach (var item in model.coke)
            {
                string query = @"
                MERGE INTO T_COKE_ALL t
                USING dual
                ON (t.BUNKER = :BUNKER AND t.CATEGORY = 'COKE')

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL

                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, C_BF, E_BF, F_BF, TOTAL, CATEGORY)
                    VALUES (:BUNKER, :C, :E, :F, :TOTAL, 'COKE')";
                
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("BUNKER", item.Bunker);
                    cmd.Parameters.Add("C", item.C ?? "0");
                    cmd.Parameters.Add("E", item.E ?? "0");
                    cmd.Parameters.Add("F", item.F ?? "0");
                    cmd.Parameters.Add("TOTAL", item.Total ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            // ============================
            // 🔷 NUT DATA
            // ============================
            foreach (var item in model.nut)
            {
                string query = @"
                MERGE INTO T_COKE_ALL t
                USING dual
                ON (t.BUNKER = :BUNKER AND t.CATEGORY = 'NUT')

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL

                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, C_BF, E_BF, F_BF, TOTAL, CATEGORY)
                    VALUES (:BUNKER, :C, :E, :F, :TOTAL, 'NUT')";
                
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("BUNKER", item.Bunker);
                    cmd.Parameters.Add("C", item.C ?? "0");
                    cmd.Parameters.Add("E", item.E ?? "0");
                    cmd.Parameters.Add("F", item.F ?? "0");
                    cmd.Parameters.Add("TOTAL", item.Total ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            trans.Commit();
            return Json("Success");
        }
        catch (Exception ex)
        {
            trans.Rollback();
            return Json("Error: " + ex.Message);
        }
    }
}