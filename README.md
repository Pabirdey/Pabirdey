  private void LoadActualFromLadle(OracleConnection con,DateTime dt,string furnace,BFViewModel model)
        {
            try
            {                
                string query = @"SELECT SUM(NET_WT) FROM DEMO.T_LADLE_DETAILS  WHERE LADLE_FLEND_TIME>=:fromDate
                                AND LADLE_FLEND_TIME <:toDate  AND DESTINATION <> 'R' AND FUR_NAME=:furnace";
                decimal actual = 0;
                using (OracleCommand cmd1 = new OracleCommand(query, con))
                {
                    cmd1.BindByName = true;
                    cmd1.Parameters.Add("fromDate",OracleDbType.Date).Value = dt.AddHours(6);
                    cmd1.Parameters.Add("toDate",OracleDbType.Date).Value =dt.AddDays(1).AddHours(6);
                    cmd1.Parameters.Add("furnace",OracleDbType.Varchar2).Value = furnace;
                    object result = cmd1.ExecuteScalar();
                    actual = result == DBNull.Value || result == null ? 0 : Convert.ToDecimal(result);
                }
                switch (furnace)
                {
                    case "C":
                        model.ActualC = actual;
                        break;
                    case "E":
                        model.ActualE = actual;
                        break;
                    case "F":
                        model.ActualF = actual;
                        break;
                }
                string tdQuery = @"SELECT DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL))ACTUAL_TD,DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED))REPORTED_TD
                                    FROM DEMO.T_BF_PRODUCTION_TRACKING  WHERE TIMESTAMP >= TRUNC(:prodDate,'MON') AND TIMESTAMP <:prodDate AND FURNACE = :furnace";
                using (OracleCommand cmd2 =new OracleCommand(tdQuery, con))
                {
                    cmd2.BindByName = true;
                    cmd2.Parameters.Add("prodDate",OracleDbType.Date).Value = dt;
                    cmd2.Parameters.Add("furnace",OracleDbType.Varchar2).Value = furnace;
                    using (OracleDataReader dr = cmd2.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            decimal? actTD=dr["ACTUAL_TD"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(dr["ACTUAL_TD"]);
                            decimal? repTD =dr["REPORTED_TD"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(dr["REPORTED_TD"]);
                            switch (furnace)
                            {                                
                                case "C":
                                    model.ACTUAL_C_TD =(actTD ?? 0)+ (model.ActualC ?? 0);
                                    model.REPORTED_C_TD=(repTD ?? 0)+ (model.ReportedC ?? 0);
                                    break;
                                case "E":
                                    model.ACTUAL_E_TD =(actTD ?? 0)+ (model.ActualE ?? 0);
                                    model.REPORTED_E_TD =(repTD ?? 0)+ (model.ReportedE ?? 0);
                                    break;                                
                                case "F":
                                    model.ACTUAL_F_TD =(actTD ?? 0)+ (model.ActualF ?? 0);
                                    model.REPORTED_F_TD =(repTD ?? 0)+ (model.ReportedF ?? 0);
                                    break;
                            }
                        }
                    }
                }
                int vday = dt.Day;                
                string balanceQuery = @"SELECT NVL(SUM(NVL(ACTUAL,0)- NVL(REPORTED,0)),0) BALANCE FROM DEMO.T_BF_PRODUCTION_TRACKING
                                       WHERE TIMESTAMP>= TRUNC(:prodDate,'MON') AND TIMESTAMP <:prodDate  AND FURNACE = :furnace";
                decimal vbal = 0;
                using (OracleCommand cmd3 = new OracleCommand(balanceQuery, con))
                {
                    cmd3.BindByName = true;
                    cmd3.Parameters.Add("prodDate",OracleDbType.Date).Value = dt;
                    cmd3.Parameters.Add("furnace",OracleDbType.Varchar2).Value = furnace;
                    object balResult = cmd3.ExecuteScalar();
                    vbal = balResult == DBNull.Value || balResult == null ? 0 : Convert.ToDecimal(balResult);
                }                
                switch (furnace)
                {
                    case "C":                        
                        if (vday == 1)
                        {
                            model.ReportedC = (model.ActualC ?? 0);                        
                        }
                        else
                        {
                            model.ReportedC = (model.ActualC ?? 0) + vbal;
                            model.REPORTED_C_TD = (repTD ?? 0) + (model.ReportedC ?? 0);
                            model.BalanceC = (model.ActualC ?? 0) - (model.ReportedC ?? 0) + vbal;
                        }
                        break;
                    case "E":
                        if (vday == 1)
                        {
                            model.ReportedE = (model.ActualE ?? 0);
                        }
                        else
                        {
                            model.ReportedE = (model.ActualE ?? 0) + vbal;
                            model.REPORTED_E_TD = (repTD ?? 0) + (model.ReportedE ?? 0);
                            model.BalanceE = (model.ActualE ?? 0) - (model.ReportedE ?? 0) + vbal;
                        }
                        break;
                    case "F":
                        if (vday == 1)
                        {
                            model.ReportedF = (model.ActualF ?? 0);
                        }
                        else
                        {
                            model.ReportedF = (model.ActualF ?? 0) + vbal;
                            model.REPORTED_F_TD = (repTD ?? 0) + (model.ReportedF ?? 0);
                            model.BalanceF = (model.ActualF ?? 0) - (model.ReportedF ?? 0) + vbal;
                        }
                        break;
                }
            }
            catch (OracleException ex)
            {
                throw new Exception(
                    $"Oracle DB Error while loading ladle data for furnace {furnace}: {ex.Message}");
            }
            catch (Exception ex)
            {
                throw new Exception(
                    $"Error while loading ladle data for furnace {furnace}: {ex.Message}");
            }
            finally
            {
                // Optional cleanup/logging
            }
        }
