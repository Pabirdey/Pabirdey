 try
            {
                using (OracleCommand cmd = new OracleCommand("DEMO.PROC_FURNACE_DERAILMENT", con))
                {
                    cmd.CommandType = CommandType.StoredProcedure;

                    cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = p_date;

                    cmd.ExecuteNonQuery();
                }
            }
            catch
            {
                // Equivalent to PL/SQL:
                // Exception
                //    When Others Then Null;
            }
