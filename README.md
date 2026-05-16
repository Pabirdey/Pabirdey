 [HttpGet]
        public JsonResult GET_CBF_TO_FBF_ReportData(string prodDate)
        {
            BFViewModel model = new BFViewModel();

            try
            {
                DateTime dt = DateTime.ParseExact(prodDate, "dd/MMM/yyyy", System.Globalization.CultureInfo.InvariantCulture);
                string formattedDate = dt.ToString("dd/MMM/yyyy").ToUpper();

                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    int vTemp = 0;
                    string countQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING  WHERE TIMESTAMP=:prodDate AND FURNACE IN ('C','E','F')";
                    using (OracleCommand cmd = new OracleCommand(countQuery, con))
                    {
                        cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = prodDate;
                        vTemp = Convert.ToInt32(cmd.ExecuteScalar());
                    }                    
                    if (vTemp > 0)
                    {
                        LoadFurnaceData(con, dt, "C", model);                        
                        LoadFurnaceData(con, dt, "E", model);
                        LoadFurnaceData(con, dt, "F", model);
                    }
                    else
                    {                        
                        LoadActualFromLadle(con, dt, "C", model);                        
                        LoadActualFromLadle(con, dt, "E", model);
                        LoadActualFromLadle(con, dt, "F", model);
                    }                    
                    LoadLadleSummary(con, dt, model);
                    model.DisplayActual=(model.ActualC ?? 0)+(model.ActualE ?? 0)+(model.ActualF ?? 0);                    
                    model.DisplayReported=(model.ReportedC ?? 0)+(model.ReportedE ?? 0)+(model.ReportedF ?? 0);                    
                    model.DisplayBalance=(model.BalanceC ?? 0)+(model.BalanceE ?? 0)+(model.BalanceF ?? 0);
                }                
                return Json(new
                {
                    success = true,
                    message = "Data loaded successfully.",
                    data = model
                }, JsonRequestBehavior.AllowGet);
            }
            catch (OracleException ex)
            {                
                return Json(new
                {
                    success = false,
                    message = "Oracle database error occurred.",
                    error = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }
            catch (Exception ex)
            {             
                return Json(new
                {
                    success = false,
                    message = "Unexpected error occurred.",
                    error = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }
            finally
            {             
            }
        }
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

        private void LoadActualFromLadle(OracleConnection con,DateTime dt,string furnace, BFViewModel model)
        {
            string query = @"SELECT SUM(NET_WT) FROM DEMO.T_LADLE_DETAILS  WHERE LADLE_FLEND_TIME>=:fromDate
                            AND LADLE_FLEND_TIME <:toDate  AND DESTINATION <> 'R'   AND FUR_NAME=:furnace";
            decimal actual = 0;
            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Parameters.Add("fromDate", OracleDbType.Date).Value = dt.AddHours(6);
                cmd.Parameters.Add("toDate", OracleDbType.Date).Value = dt.AddDays(1).AddHours(6);
                cmd.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;
                object result = cmd.ExecuteScalar();
                actual = result == DBNull.Value ? 0 : Convert.ToDecimal(result);
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
        }
        private void LoadLadleSummary(OracleConnection con,DateTime dt, BFViewModel model)
        {
            string query = @"SELECT NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT END),0) LD1,
                                    NVL(SUM(CASE WHEN DESTINATION='LD2' THEN NET_WT END),0) LD2,
                                    NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT END),0) LD3,
                                    NVL(SUM(CASE WHEN DESTINATION='MRD' THEN NET_WT END),0) MRD,
                                    NVL(SUM(FILL_STATUS),0) TP  FROM DEMO.T_LADLE_DETAILS
                                    WHERE LADLE_FLEND_TIME>=:fromDate  AND LADLE_FLEND_TIME<:toDate
                                    AND FUR_NAME IN ('C','E','F')";
            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Parameters.Add("fromDate", OracleDbType.Date).Value = dt.AddHours(6);
                cmd.Parameters.Add("toDate", OracleDbType.Date).Value = dt.AddDays(1).AddHours(6);
                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    if (dr.Read())
                    {
                        model.LD1Tons = Convert.ToDecimal(dr["LD1"]);
                        model.LD2Tons = Convert.ToDecimal(dr["LD2"]);
                        model.LD3Tons = Convert.ToDecimal(dr["LD3"]);
                        model.MRDTPTons = Convert.ToDecimal(dr["MRD"]);
                        model.NoOfTP = Convert.ToInt32(dr["TP"]);
                    }
                }
            }
        }

  <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_C" readonly /></td>                                            <td><input type="text" class="form-control" id="ACTUAL_C" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_C_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_C" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_C_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="BALANCE_C" readonly /></td>                                           
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_E" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_E" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="BALANCE_E" readonly /></td> 
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_F" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_F" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_F_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_F" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_F_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="BALANCE_F" readonly /></td> 
                                        </tr>
