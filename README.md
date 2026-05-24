  [HttpPost]
        public JsonResult SaveBFProdData(List<BFViewModel> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    for (int i = 0; i < modelList.Count; i++)
                    {
                        BFViewModel model = modelList[i];
                        string checkQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING  WHERE FURNACE=:FURNACE  AND TIMESTAMP=:TIMESTAMP";
                        int count = 0;
                        using (OracleCommand cmd = new OracleCommand(checkQuery, con))
                        {
                            cmd.BindByName = true;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                            cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);
                            count = Convert.ToInt32(cmd.ExecuteScalar());
                        }
                        if (count > 0)
                        {
                            string updateQuery = @"UPDATE DEMO.T_BF_PRODUCTION_TRACKING
                                    SET
                                        ACTUAL = :ACTUAL,
                                        REPORTED = :REPORTED,
                                        BALANCE = :BALANCE
                                    WHERE  FURNACE=:FURNACE AND TIMESTAMP=:TIMESTAMP";
                            using (OracleCommand cmd = new OracleCommand(updateQuery, con))
                            {
                                cmd.BindByName = true;
                                cmd.Parameters.Add("ACTUAL", OracleDbType.Decimal).Value = model.ACTUAL;
                                cmd.Parameters.Add("REPORTED", OracleDbType.Decimal).Value = model.REPORTED;
                                cmd.Parameters.Add("BALANCE", OracleDbType.Decimal).Value = model.BALANCE;
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                                cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);
                                cmd.ExecuteNonQuery();
                            }
                        }
                        else
                        {
                            string insertQuery = @"INSERT INTO DEMO.T_BF_PRODUCTION_TRACKING(FURNACE,TIMESTAMP,ACTUAL,REPORTED,BALANCE)
                                                VALUES(:FURNACE,:TIMESTAMP,:ACTUAL,:REPORTED,:BALANCE)";
                            using (OracleCommand cmd = new OracleCommand(insertQuery, con))
                            {
                                cmd.BindByName = true;
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                                cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);
                                cmd.Parameters.Add("ACTUAL", OracleDbType.Decimal).Value = model.ACTUAL;
                                cmd.Parameters.Add("REPORTED", OracleDbType.Decimal).Value = model.REPORTED;
                                cmd.Parameters.Add("BALANCE", OracleDbType.Decimal).Value = model.BALANCE;
                                cmd.ExecuteNonQuery();
                            }
                        }
                    }
                }

                return Json(new
                {
                    success = true,
                    message = "Data Saved Successfully"
                });
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
