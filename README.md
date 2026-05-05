    public JsonResult SaveFurnaceCokeUnloading(Furnace_High_line model)
        {
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                OracleTransaction trans = con.BeginTransaction();

                try
                {
                    
                    foreach (var item in model.main)
                    {
                        string query = @"
                MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                USING dual
                ON (t.TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY') 
                    AND t.SHIFT = :SHIFT 
                    AND t.BUNKER = :BUNKER)

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C = :C,
                        t.E = :E,
                        t.F = :F,
                        t.TOTAL = :TOTAL,
                        t.BUNKER_POSITION = :POSITION,
                        t.BALANCE = :BALANCE

                WHEN NOT MATCHED THEN
                    INSERT (TIMESTAMP, SHIFT, BUNKER, C, E, F, TOTAL, BUNKER_POSITION, BALANCE)
                    VALUES (TO_DATE(:TDATE,'DD/MM/YYYY'), :SHIFT, :BUNKER, :C, :E, :F, :TOTAL, :POSITION, :BALANCE)";

                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;

                            cmd.Parameters.Add("TIMESTAMP", item.Date);
                            cmd.Parameters.Add("SHIFT", item.Shift);
                            cmd.Parameters.Add("BUNKER", item.Bunker);

                            cmd.Parameters.Add("C", item.C ?? "0");
                            cmd.Parameters.Add("E", item.E ?? "0");
                            cmd.Parameters.Add("F", item.F ?? "0");
                            cmd.Parameters.Add("TOTAL", item.Total ?? "0");

                            cmd.Parameters.Add("BUNKER_POSITION", item.Position ?? "0");
                            cmd.Parameters.Add("BALANCE", item.Balance ?? "0");

                            cmd.ExecuteNonQuery();
                        }
                    }

                   
                    foreach (var item in model.coke)
                    {
                        string query = @"
                MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                USING dual
                ON (t.BUNKER = :BUNKER )

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.TON_C_SC = :C,
                        t.TON_E_SC = :E,
                        t.TON_F_SC = :F                       

                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, TON_C_SC, TON_E_SC, TON_F_SC)
                    VALUES (:BUNKER, :C, :E, :F)";

                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;

                            cmd.Parameters.Add("BUNKER", item.Bunker);
                            cmd.Parameters.Add("TON_C_SC", item.C ?? "0");
                            cmd.Parameters.Add("TON_E_SC", item.E ?? "0");
                            cmd.Parameters.Add("TON_F_SC", item.F ?? "0");                           
                            cmd.ExecuteNonQuery();
                        }
                    }

                   
                    foreach (var item in model.nut)
                    {
                        string query = @"
                MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                USING dual
                ON (t.BUNKER = :BUNKER)

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.TON_C_NC = :C,
                        t.TON_E_NC = :E,
                        t.TON_F_NC = :F                       
                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, TON_C_NC, TON_E_NC, TON_F_NC)
                    VALUES (:BUNKER, :C, :E, :F)";

                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;

                            cmd.Parameters.Add("BUNKER", item.Bunker);
                            cmd.Parameters.Add("TON_C_NC", item.C ?? "0");
                            cmd.Parameters.Add("TON_E_NC", item.E ?? "0");
                            cmd.Parameters.Add("TON_F_NC", item.F ?? "0");                           
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
