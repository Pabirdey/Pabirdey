[HttpPost]
public JsonResult CalculateHMTPOT(List<BFViewModel> modelList)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            foreach (var model in modelList)
            {
                // Only process C,D,E,F
                if (!new[] { "C", "D", "E", "F" }.Contains(model.FURNACE))
                    continue;

                using (OracleTransaction trans = con.BeginTransaction())
                {
                    try
                    {
                        decimal vTotalTP = 0;
                        decimal vTotalOT = 0;
                        decimal vTotProdTP = 0;
                        decimal vTotProdOT = 0;
                        decimal? vHMTTP = null;
                        decimal? vHMTOT = null;

                        //--------------------------------------------------
                        // Get TP & OT Count
                        //--------------------------------------------------
                        string sql = @"SELECT NVL(NOOFTP,0),
                                              NVL(NOOFOT,0)
                                       FROM DEMO.T_LADLE
                                       WHERE DATE_TIME = :P_DATE
                                       AND PLANT='A-F'";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                            using (OracleDataReader dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    vTotalTP = Convert.ToDecimal(dr[0]);
                                    vTotalOT = Convert.ToDecimal(dr[1]);
                                }
                            }
                        }

                        //--------------------------------------------------
                        // TP Production
                        //--------------------------------------------------
                        sql = @"SELECT NVL(SUM(NET_WT),0)
                                FROM DEMO.T_LADLE_DETAILS
                                WHERE TIMESTAMP=:P_DATE
                                AND TRP_NO < 52";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                            vTotProdTP = Convert.ToDecimal(cmd.ExecuteScalar());
                        }

                        //--------------------------------------------------
                        // OT Production
                        //--------------------------------------------------
                        sql = @"SELECT NVL(SUM(NET_WT),0)
                                FROM DEMO.T_LADLE_DETAILS
                                WHERE TIMESTAMP=:P_DATE
                                AND TRP_NO > 51";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                            vTotProdOT = Convert.ToDecimal(cmd.ExecuteScalar());
                        }

                        //--------------------------------------------------
                        // Calculation
                        //--------------------------------------------------
                        if (vTotalTP > 0)
                            vHMTTP = Math.Round(vTotProdTP / vTotalTP, 2);

                        if (vTotalOT > 0)
                            vHMTOT = Math.Round(vTotProdOT / vTotalOT, 2);

                        //--------------------------------------------------
                        // Update
                        //--------------------------------------------------
                        sql = @"UPDATE DEMO.T_LADLE
                                SET HM_TONS_PER_OT=:P_OT,
                                    HM_TONS_PER_TP=:P_TP
                                WHERE DATE_TIME=:P_DATE
                                AND PLANT='A-F'";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Transaction = trans;

                            cmd.Parameters.Add("P_OT", OracleDbType.Decimal).Value =
                                (object)vHMTOT ?? DBNull.Value;

                            cmd.Parameters.Add("P_TP", OracleDbType.Decimal).Value =
                                (object)vHMTTP ?? DBNull.Value;

                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value =
                                Convert.ToDateTime(model.PROD_DATE);

                            cmd.ExecuteNonQuery();
                        }

                        //--------------------------------------------------
                        // Procedure Call
                        //--------------------------------------------------
                        using (OracleCommand cmd = new OracleCommand("DEMO.PROC_LADLE_TODATE", con))
                        {
                            cmd.Transaction = trans;
                            cmd.CommandType = CommandType.StoredProcedure;

                            cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value =
                                Convert.ToDateTime(model.PROD_DATE);

                            cmd.ExecuteNonQuery();
                        }

                        trans.Commit();
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

            return Json(new
            {
                success = true,
                message = "Calculation completed successfully."
            });
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