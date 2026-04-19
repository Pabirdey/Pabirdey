public JsonResult SaveData(MyModel model)
{
    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        using (OracleTransaction trans = con.BeginTransaction())
        {
            try
            {
                int count = 0;

                // ================= 1. T_BF_PRODUCTION_TRACKING =================
                string count1 = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING 
                                  WHERE TIMESTAMP = :DATE_TIME AND FURNACE = :FURNACE";

                using (OracleCommand cmd = new OracleCommand(count1, con))
                {
                    cmd.Transaction = trans;
                    cmd.Parameters.Add("DATE_TIME", OracleDbType.Date).Value = model.DATE_TIME_PROD_C;
                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE_C;

                    count = Convert.ToInt32(cmd.ExecuteScalar());
                }

                if (count > 0)
                {
                    string update = @"UPDATE DEMO.T_BF_PRODUCTION_TRACKING 
                                      SET ACTUAL=:ACTUAL, REPORTED=:REPORTED, BALANCE=:BALANCE
                                      WHERE TIMESTAMP=:DATE_TIME AND FURNACE=:FURNACE";

                    using (OracleCommand cmd = new OracleCommand(update, con))
                    {
                        cmd.Transaction = trans;

                        cmd.Parameters.Add("ACTUAL", model.ACTUAL_C);
                        cmd.Parameters.Add("REPORTED", model.REPORTED_C);
                        cmd.Parameters.Add("BALANCE", model.BALANCE_C);
                        cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_C);
                        cmd.Parameters.Add("FURNACE", model.FURNACE_C);

                        cmd.ExecuteNonQuery();
                    }
                }
                else
                {
                    string insert = @"INSERT INTO DEMO.T_BF_PRODUCTION_TRACKING
                                    (TIMESTAMP,FURNACE,ACTUAL,REPORTED,BALANCE)
                                    VALUES(:DATE_TIME,:FURNACE,:ACTUAL,:REPORTED,:BALANCE)";

                    using (OracleCommand cmd = new OracleCommand(insert, con))
                    {
                        cmd.Transaction = trans;

                        cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_C);
                        cmd.Parameters.Add("FURNACE", model.FURNACE_C);
                        cmd.Parameters.Add("ACTUAL", model.ACTUAL_C);
                        cmd.Parameters.Add("REPORTED", model.REPORTED_C);
                        cmd.Parameters.Add("BALANCE", model.BALANCE_C);

                        cmd.ExecuteNonQuery();
                    }
                }

                // ================= 2. T_LADLE =================
                string count2 = @"SELECT COUNT(*) FROM DEMO.T_LADLE 
                                  WHERE DATE_TIME=:DATE_TIME AND PLANT='A-F'";

                using (OracleCommand cmd = new OracleCommand(count2, con))
                {
                    cmd.Transaction = trans;
                    cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_F);
                    count = Convert.ToInt32(cmd.ExecuteScalar());
                }

                if (count > 0)
                {
                    string update = @"UPDATE DEMO.T_LADLE SET 
                                    DATE_TIME=:DATE_TIME,
                                    LD1_TONS=:LD1,
                                    LD2_TONS=:LD2,
                                    LD3_TONS=:LD3,
                                    MRDTP_TONS=:MRDTP,
                                    NOOFTP=:NOOFTP
                                    WHERE DATE_TIME=:DATE_TIME_PROD_F AND PLANT='A-F'";

                    using (OracleCommand cmd = new OracleCommand(update, con))
                    {
                        cmd.Transaction = trans;

                        cmd.Parameters.Add("DATE_TIME", model.DATE_TIME);
                        cmd.Parameters.Add("LD1", model.LD1_TONS);
                        cmd.Parameters.Add("LD2", model.LD2_TONS);
                        cmd.Parameters.Add("LD3", model.LD3_TONS);
                        cmd.Parameters.Add("MRDTP", model.MRDTP_TONS);
                        cmd.Parameters.Add("NOOFTP", model.NOOFTP);
                        cmd.Parameters.Add("DATE_TIME_PROD_F", model.DATE_TIME_PROD_F);

                        cmd.ExecuteNonQuery();
                    }
                }
                else
                {
                    string insert = @"INSERT INTO DEMO.T_LADLE
                    (DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,
                     LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL,PLANT)
                    VALUES(:DATE_TIME,:LD1,:LD2,:LD3,:MRDTP,:NOOFTP,
                           :LD1A,:LD2A,:LD3A,:MRDTPA,'A-F')";

                    using (OracleCommand cmd = new OracleCommand(insert, con))
                    {
                        cmd.Transaction = trans;

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
                }

                // ================= 3. T_BF_PRODUCTION_TEST =================
                string count3 = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TEST 
                                  WHERE TIMESTAMP=:DATE_TIME AND FUR_NO=:FURNACE";

                using (OracleCommand cmd = new OracleCommand(count3, con))
                {
                    cmd.Transaction = trans;
                    cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_C);
                    cmd.Parameters.Add("FURNACE", model.FURNACE_C);

                    count = Convert.ToInt32(cmd.ExecuteScalar());
                }

                if (count > 0)
                {
                    string update = @"UPDATE DEMO.T_BF_PRODUCTION_TEST 
                                      SET PRODUCTION=:PROD
                                      WHERE TIMESTAMP=:DATE_TIME AND FUR_NO=:FURNACE";

                    using (OracleCommand cmd = new OracleCommand(update, con))
                    {
                        cmd.Transaction = trans;

                        cmd.Parameters.Add("PROD", model.REPORTED_C);
                        cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_C);
                        cmd.Parameters.Add("FURNACE", model.FURNACE_C);

                        cmd.ExecuteNonQuery();
                    }
                }
                else
                {
                    string insert = @"INSERT INTO DEMO.T_BF_PRODUCTION_TEST
                                      (TIMESTAMP,FUR_NO,PRODUCTION)
                                      VALUES(:DATE_TIME,:FURNACE,:PROD)";

                    using (OracleCommand cmd = new OracleCommand(insert, con))
                    {
                        cmd.Transaction = trans;

                        cmd.Parameters.Add("DATE_TIME", model.DATE_TIME_PROD_C);
                        cmd.Parameters.Add("FURNACE", model.FURNACE_C);
                        cmd.Parameters.Add("PROD", model.REPORTED_C);

                        cmd.ExecuteNonQuery();
                    }
                }

                trans.Commit();

                return Json(new { success = true });
            }
            catch (Exception ex)
            {
                trans.Rollback();
                return Json(new { success = false, message = ex.Message });
            }
        }
    }
}
