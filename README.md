[HttpPost]
public JsonResult CalculateHMTPOT(DateTime productionDate)
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
                    decimal? vTotalTP = null;
                    decimal? vTotalOT = null;
                    decimal? vTotProdTP = null;
                    decimal? vTotProdOT = null;
                    decimal? vHMT_TP = null;
                    decimal? vHMT_OT = null;

                    // Get TP and OT
                    try
                    {
                        string sql = @"SELECT NOOFTP, NOOFOT
                                       FROM DEMO.T_LADLE
                                       WHERE DATE_TIME = :P_DATE
                                       AND PLANT = 'A-F'";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = productionDate;

                            using (OracleDataReader dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    vTotalTP = dr.IsDBNull(0) ? (decimal?)null : Convert.ToDecimal(dr[0]);
                                    vTotalOT = dr.IsDBNull(1) ? (decimal?)null : Convert.ToDecimal(dr[1]);
                                }
                            }
                        }
                    }
                    catch
                    {
                        vTotalTP = null;
                        vTotalOT = null;
                    }

                    // Total Production TP
                    try
                    {
                        string sql = @"SELECT SUM(NET_WT)
                                       FROM DEMO.T_LADLE_DETAILS
                                       WHERE TIMESTAMP = :P_DATE
                                       AND TRP_NO < 52";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = productionDate;

                            object result = cmd.ExecuteScalar();
                            if (result != DBNull.Value && result != null)
                                vTotProdTP = Convert.ToDecimal(result);
                        }
                    }
                    catch
                    {
                        vTotProdTP = null;
                    }

                    // HM Tons Per TP
                    try
                    {
                        if (vTotalTP.HasValue && vTotalTP.Value != 0 &&
                            vTotProdTP.HasValue)
                        {
                            vHMT_TP = Math.Round(vTotProdTP.Value / vTotalTP.Value, 2);
                        }
                    }
                    catch
                    {
                        vHMT_TP = null;
                    }

                    // Total Production OT
                    try
                    {
                        string sql = @"SELECT SUM(NET_WT)
                                       FROM DEMO.T_LADLE_DETAILS
                                       WHERE TIMESTAMP = :P_DATE
                                       AND TRP_NO > 51";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = productionDate;

                            object result = cmd.ExecuteScalar();
                            if (result != DBNull.Value && result != null)
                                vTotProdOT = Convert.ToDecimal(result);
                        }
                    }
                    catch
                    {
                        vTotProdOT = null;
                    }

                    // HM Tons Per OT
                    try
                    {
                        if (vTotalOT.HasValue && vTotalOT.Value != 0 &&
                            vTotProdOT.HasValue)
                        {
                            vHMT_OT = Math.Round(vTotProdOT.Value / vTotalOT.Value, 2);
                        }
                    }
                    catch
                    {
                        vHMT_OT = null;
                    }

                    // Update T_LADLE
                    string updateSql = @"UPDATE DEMO.T_LADLE
                                         SET HM_TONS_PER_OT = :P_OT,
                                             HM_TONS_PER_TP = :P_TP
                                         WHERE DATE_TIME = :P_DATE
                                         AND PLANT = 'A-F'";

                    using (OracleCommand cmd = new OracleCommand(updateSql, con))
                    {
                        cmd.Transaction = trans;
                        cmd.Parameters.Add(":P_OT", OracleDbType.Decimal).Value = (object)vHMT_OT ?? DBNull.Value;
                        cmd.Parameters.Add(":P_TP", OracleDbType.Decimal).Value = (object)vHMT_TP ?? DBNull.Value;
                        cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = productionDate;

                        cmd.ExecuteNonQuery();
                    }

                    // Call Procedure
                    try
                    {
                        using (OracleCommand cmd = new OracleCommand("DEMO.PROC_LADLE_TODATE", con))
                        {
                            cmd.Transaction = trans;
                            cmd.CommandType = CommandType.StoredProcedure;

                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = productionDate;

                            cmd.ExecuteNonQuery();
                        }
                    }
                    catch
                    {
                        // Ignore procedure errors
                    }

                    trans.Commit();

                    return Json(new
                    {
                        success = true,
                        message = "Calculation completed successfully."
                    });
                }
                catch (Exception ex)
                {
                    trans.Rollback();

                    return Json(new
                    {
                        success = false,
                        message = ex.Message
                    });
                }
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