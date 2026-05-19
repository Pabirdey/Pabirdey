 [HttpPost]
        public JsonResult SaveDEMOBFProdData(List<BFViewModel> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    for (int i = 0; i < modelList.Count; i++)
                    {
                        BFViewModel model = modelList[i];
                        string checkQuery = @"SELECT COUNT(*) FROM TEST.T_BF_PRODUCTION_TEST  WHERE FURNACE=:FURNACE  AND TIMESTAMP=:TIMESTAMP";
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
                            string updateQuery = @"UPDATE TEST.T_BF_PRODUCTION_TEST
                                    SET                                       
                                        PRODUCTION = :REPORTED                                        
                                    WHERE  FURNACE=:FURNACE AND TIMESTAMP=:TIMESTAMP";
                            using (OracleCommand cmd = new OracleCommand(updateQuery, con))
                            {
                                cmd.BindByName = true;                                
                                cmd.Parameters.Add("PRODUCTION", OracleDbType.Decimal).Value = model.REPORTED;                                
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                                cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);
                                cmd.ExecuteNonQuery();
                            }
                        }
                        else
                        {
                            string insertQuery = @"INSERT INTO TEST.T_BF_PRODUCTION_TRACKING(FURNACE,TIMESTAMP,PRODUCTION)
                                                VALUES(:FURNACE,:TIMESTAMP,:REPORTED)";
                            using (OracleCommand cmd = new OracleCommand(insertQuery, con))
                            {
                                cmd.BindByName = true;
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                                cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);                                
                                cmd.Parameters.Add("REPORTED", OracleDbType.Decimal).Value = model.REPORTED;                                
                                cmd.ExecuteNonQuery();
                            }
                        }
                    }
                }

                return Json(new
                {
                    success = true,
                    message = "Data BF Prod Saved Successfully"
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
