 public JsonResult GET_GBF_IBF_ACTUAL_REPORT(string prodDate)
        {
            BFViewModel model = new BFViewModel();
            model.Furnaces = new List<GBFTOIBFPRODUCTION>();
            try
            {
                DateTime dt = DateTime.ParseExact(prodDate, "dd/MMM/yyyy", System.Globalization.CultureInfo.InvariantCulture);               
                string[] furnaces = { "G", "H", "I" };
                using (OracleConnection con =new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    foreach (string furnace in furnaces)
                    {
                        try
                        {
                            GBFTOIBFPRODUCTION row =new GBFTOIBFPRODUCTION();
                            row.FURNACE = furnace;
                            int count = 0;                            
                            string chkQry = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING  WHERE TIMESTAMP=:PDATE  AND FURNACE=:FURNACE";
                            using (OracleCommand chkCmd =new OracleCommand(chkQry, con))
                            {
                                chkCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                                chkCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                                count = Convert.ToInt32(chkCmd.ExecuteScalar());
                            }                          
                            
                            if (count > 0)
                            {
                                string qry = @"SELECT NVL(ACTUAL,0),NVL(REPORTED,0),NVL(BALANCE,0)  FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP=:PDATE  AND FURNACE=:FURNACE";
                                using (OracleCommand cmd =new OracleCommand(qry, con))
                                {
                                    cmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                                    cmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                                    OracleDataReader dr =cmd.ExecuteReader();
                                    if (dr.Read())
                                    {
                                        row.ACTUAL=Convert.ToDecimal(dr[0] == DBNull.Value ? 0 : dr[0]);
                                        row.REPORTED =Convert.ToDecimal(dr[1] == DBNull.Value ? 0 : dr[1]);
                                        row.BALANCE =Convert.ToDecimal(dr[2] == DBNull.Value ? 0 : dr[2]);
                                    }
                                    dr.Close();
                                }
                            }
                            
                            else
                            {
                                string actualQry = @"SELECT NVL(SUM(NET_WT),0) FROM DEMO.T_LADLE_DETAILS  
                                                     WHERE LADLE_FLEND_TIME>=:FROMDATE AND LADLE_FLEND_TIME<:TODATE
                                                     AND DESTINATION <> 'R' AND FUR_NAME = :FURNACE";
                                using (OracleCommand actualCmd =new OracleCommand(actualQry, con))
                                {
                                    actualCmd.Parameters.Add("FROMDATE",OracleDbType.Date).Value =dt.AddHours(6);
                                    actualCmd.Parameters.Add("TODATE",OracleDbType.Date).Value =dt.AddDays(1).AddHours(6);
                                    actualCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value =furnace;
                                    row.ACTUAL = Convert.ToDecimal(actualCmd.ExecuteScalar());
                                }

                                string balQry = @"SELECT NVL(SUM(NVL(ACTUAL,0)-NVL(REPORTED,0)),0)  FROM DEMO.T_BF_PRODUCTION_TRACKING
                                                WHERE TIMESTAMP>=TRUNC(:PDATE,'MON') AND TIMESTAMP <:PDATE  AND FURNACE=:FURNACE";
                                using (OracleCommand balCmd =new OracleCommand(balQry, con))
                                {
                                    balCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                                    balCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value =furnace;
                                    row.BALANCE =Convert.ToDecimal(balCmd.ExecuteScalar());
                                }
                                row.REPORTED=row.ACTUAL + row.BALANCE;
                                row.BALANCE =row.ACTUAL -row.REPORTED +row.BALANCE;
                            }
                            
                            string tdQry = @"SELECT   NVL(SUM(ACTUAL),0),NVL(SUM(REPORTED),0) FROM DEMO.T_BF_PRODUCTION_TRACKING
                                            WHERE TIMESTAMP>=TRUNC(:PDATE,'MON') AND TIMESTAMP<:PDATE  AND FURNACE=:FURNACE";
                            decimal prevActual = 0;
                            decimal prevReported = 0;
                            using (OracleCommand tdCmd =new OracleCommand(tdQry, con))
                            {
                                tdCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                                tdCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value=furnace;
                                OracleDataReader tdDr =tdCmd.ExecuteReader();
                                if (tdDr.Read())
                                {
                                    prevActual=Convert.ToDecimal(tdDr[0] == DBNull.Value ? 0 : tdDr[0]);
                                    prevReported=Convert.ToDecimal(tdDr[1] == DBNull.Value ? 0 : tdDr[1]);
                                }

                                tdDr.Close();
                            }

                            row.ACTUAL_TD =prevActual + row.ACTUAL;
                            row.REPORTED_TD=prevReported + row.REPORTED;                            
                            LoadLadleData(con, dt, furnace, row);                            
                            model.DISPLAY_ACTUAL += row.ACTUAL;
                            model.DISPLAY_REPORTED += row.REPORTED;
                            model.DISPLAY_BALANCE += row.BALANCE;
                            model.DISPLAY_ACTUAL_TD += row.ACTUAL_TD;
                            model.DISPLAY_REPORTED_TD += row.REPORTED_TD;
                            model.Furnaces.Add(row);
                        }
                        catch (Exception ex)
                        {
                            return Json(new
                            {
                                success = false,
                                message = "Error in Furnace : "
                                          + furnace +
                                          " -> " +
                                          ex.Message
                            },
                            JsonRequestBehavior.AllowGet);
                        }
                    }
                }

                return Json(new
                {
                    success = true,
                    data = model
                },
                JsonRequestBehavior.AllowGet);
            }
            catch (Exception ex)
            {
                return Json(new
                {
                    success = false,
                    message = ex.Message
                },
                JsonRequestBehavior.AllowGet);
            }
        }
