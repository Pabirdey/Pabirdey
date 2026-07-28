[HttpPost]
public JsonResult SaveLadleData(List<BFViewModel> modelList)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            OracleTransaction tran = con.BeginTransaction();

            try
            {
                foreach (BFViewModel model in modelList)
                {
                    int vCount = 0;

                    #region CHECK RECORD

                    string checkSql = @"SELECT COUNT(*)
                                        FROM DEMO.T_LADLE
                                        WHERE DATE_TIME = :P_DATE
                                        AND PLANT='G'";

                    using (OracleCommand cmd = new OracleCommand(checkSql, con))
                    {
                        cmd.Transaction = tran;

                        cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = model.PROD_DATE;

                        vCount = Convert.ToInt32(cmd.ExecuteScalar());
                    }

                    #endregion

                    if (vCount > 0)
                    {
                        #region UPDATE

                        string updateSql = @"UPDATE DEMO.T_LADLE
                                             SET DATE_TIME = :P_DATE,
                                                 LD1_TONS = NULL,
                                                 LD2_TONS = NULL,
                                                 LD3_TONS = NULL,
                                                 MRDTP_TONS = NULL,
                                                 NOOFTP = :P_NOOFTP
                                             WHERE DATE_TIME = :P_DATE
                                             AND PLANT='G'";

                        using (OracleCommand cmd = new OracleCommand(updateSql, con))
                        {
                            cmd.Transaction = tran;

                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = model.PROD_DATE;
                            cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Decimal).Value = model.NOOFTP_G;

                            cmd.ExecuteNonQuery();
                        }

                        #endregion
                    }
                    else
                    {
                        #region INSERT

                        string insertSql = @"INSERT INTO DEMO.T_LADLE
                                            (
                                                DATE_TIME,
                                                LD1_TONS,
                                                LD2_TONS,
                                                LD3_TONS,
                                                MRDTP_TONS,
                                                NOOFTP,
                                                LD1_TONS_ACTUAL,
                                                LD2_TONS_ACTUAL,
                                                LD3_TONS_ACTUAL,
                                                MRDTP_TONS_ACTUAL,
                                                PLANT
                                            )
                                            VALUES
                                            (
                                                :P_DATE,
                                                NULL,
                                                NULL,
                                                NULL,
                                                NULL,
                                                :P_NOOFTP,
                                                :P_LD1_ACTUAL,
                                                :P_LD2_ACTUAL,
                                                :P_LD3_ACTUAL,
                                                :P_MRDTP_ACTUAL,
                                                'G'
                                            )";

                        using (OracleCommand cmd = new OracleCommand(insertSql, con))
                        {
                            cmd.Transaction = tran;

                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = model.PROD_DATE;
                            cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Decimal).Value = model.NOOFTP_G;

                            cmd.Parameters.Add(":P_LD1_ACTUAL", OracleDbType.Decimal).Value = model.LD1_TONS_ACTUAL_G;
                            cmd.Parameters.Add(":P_LD2_ACTUAL", OracleDbType.Decimal).Value = model.LD2_TONS_ACTUAL_G;
                            cmd.Parameters.Add(":P_LD3_ACTUAL", OracleDbType.Decimal).Value = model.LD3_TONS_ACTUAL_G;
                            cmd.Parameters.Add(":P_MRDTP_ACTUAL", OracleDbType.Decimal).Value = model.MRDTP_TONS_ACTUAL_G;

                            cmd.ExecuteNonQuery();
                        }

                        #endregion
                    }
                }

                tran.Commit();

                return Json(new
                {
                    success = true,
                    message = "Data Saved Successfully."
                });
            }
            catch (Exception ex)
            {
                tran.Rollback();

                return Json(new
                {
                    success = false,
                    message = ex.Message
                });
            }
        }
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        });
    }
}
