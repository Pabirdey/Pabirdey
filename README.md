[HttpPost]
        public JsonResult CalculateHMTPOT(List<BFViewModel> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    for (int i = 0; i < modelList.Count; i++)
                    {
                        BFViewModel model = modelList[i];
                        if (model.FURNACE != "C" && model.FURNACE != "D" && model.FURNACE != "E" && model.FURNACE != "F")
                        {
                            continue;
                        }

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

                                try
                                {
                                    string sql = @"SELECT NOOFTP,NOOFOT FROM DEMO.T_LADLE WHERE DATE_TIME = :P_DATE AND PLANT = 'A-F'";
                                    using (OracleCommand cmd = new OracleCommand(sql, con))
                                    {
                                        cmd.Transaction = trans;
                                        cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

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


                                try
                                {
                                    string sql = @"SELECT SUM(NET_WT)
                                       FROM DEMO.T_LADLE_DETAILS
                                       WHERE TIMESTAMP = :P_DATE
                                       AND TRP_NO < 52";

                                    using (OracleCommand cmd = new OracleCommand(sql, con))
                                    {
                                        cmd.Transaction = trans;
                                        cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                                        object result = cmd.ExecuteScalar();
                                        if (result != DBNull.Value && result != null)
                                            vTotProdTP = Convert.ToDecimal(result);
                                    }
                                }
                                catch
                                {
                                    vTotProdTP = null;
                                }


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


                                try
                                {
                                    string sql = @"SELECT SUM(NET_WT)
                                       FROM DEMO.T_LADLE_DETAILS
                                       WHERE TIMESTAMP = :P_DATE
                                       AND TRP_NO > 51";

                                    using (OracleCommand cmd = new OracleCommand(sql, con))
                                    {
                                        cmd.Transaction = trans;
                                        cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                                        object result = cmd.ExecuteScalar();
                                        if (result != DBNull.Value && result != null)
                                            vTotProdOT = Convert.ToDecimal(result);
                                    }
                                }
                                catch
                                {
                                    vTotProdOT = null;
                                }


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
                                    

                                    cmd.ExecuteNonQuery();
                                }


                                try
                                {
                                    using (OracleCommand cmd = new OracleCommand("DEMO.PROC_LADLE_TODATE", con))
                                    {
                                        cmd.Transaction = trans;
                                        cmd.CommandType = CommandType.StoredProcedure;

                                        cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);

                                        cmd.ExecuteNonQuery();
                                    }
                                }
                                catch
                                {

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
         function Save_A_FBF_CalculateHMTPOT(modelList) {
        $.ajax({
            url: '/BF_Production/CalculateHMTPOT',
            type: 'POST',
            data: JSON.stringify(modelList),
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            success: function (res) {
                if (res.success) {
                    alert("BF Prod Save Data Successfully");                                       
                }
                else {
                    alert(res.message);
                }
            },

            error: function (xhr) {
                alert("Server Error");
                console.log(xhr.responseText);
            }
        });
    }
