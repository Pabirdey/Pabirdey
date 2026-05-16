private void LoadFurnaceData(OracleConnection con,DateTime dt,string furnace, BFViewModel model)
        {
            try
            {
                string query = @"SELECT ACTUAL, REPORTED, BALANCE FROM DEMO.T_BF_PRODUCTION_TRACKING  WHERE TIMESTAMP=:prodDate   AND FURNACE=:furnace";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = dt;
                    cmd.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;
                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            decimal actual = dr["ACTUAL"] == DBNull.Value ? 0: Convert.ToDecimal(dr["ACTUAL"]);
                            decimal reported = dr["REPORTED"] == DBNull.Value ? 0: Convert.ToDecimal(dr["REPORTED"]);
                            decimal balance = dr["BALANCE"] == DBNull.Value ? 0: Convert.ToDecimal(dr["BALANCE"]);
                            switch (furnace)
                            {
                                case "C":
                                    model.ActualC = actual;
                                    model.ReportedC = reported;
                                    model.BalanceC = balance;
                                    break;                              
                                case "E":
                                    model.ActualE = actual;
                                    model.ReportedE = reported;
                                    model.BalanceE = balance;
                                    break;
                                case "F":
                                    model.ActualF = actual;
                                    model.ReportedF = reported;
                                    model.BalanceF = balance;
                                    break;
                            }
                        }
                    }
                    string tdQuery= @"SELECT DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL)),DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED))
                                    FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP >= TRUNC(:prodDate,'MON') AND TIMESTAMP<=:prodDate AND FURNACE=:furnace";
                    using (OracleCommand cmd = new OracleCommand(tdQuery, con))
                    {
                        cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = dt;

                        using (OracleDataReader dr = cmd.ExecuteReader())
                        {
                            if (dr.Read())
                            {
                                decimal ActTD = dr[0] == DBNull.Value ? 0 : Convert.ToDecimal(dr[0]);
                                decimal RepTD = dr[1] == DBNull.Value ? 0 : Convert.ToDecimal(dr[1]);
                                switch (furnace)
                                {
                                    case "C":
                                        model.ACTUAL_C_TD = ActTD;
                                        model.REPORTED_C_TD = RepTD;                                       
                                        break;
                                    case "E":
                                        model.ACTUAL_E_TD = ActTD;
                                        model.REPORTED_E_TD = RepTD;
                                        break;
                                    case "F":
                                        model.ACTUAL_F_TD = ActTD;
                                        model.REPORTED_F_TD = RepTD;
                                        break;
                                }
                            }
                        }
                    }

                }
            }
            catch (OracleException ex)
            {
                
                throw new Exception(
                    $"Oracle DB Error while loading furnace {furnace}: {ex.Message}");
            }
            catch (Exception ex)
            {
               
                throw new Exception(
                    $"Error while loading furnace {furnace}: {ex.Message}");
            }
            finally
            {
              
            }
        }
