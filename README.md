 [HttpPost]
        public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
        {
            RmbbPile model = new RmbbPile();
            string message = "";
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {

                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();


                    string checkSql = "SELECT COUNT(*) FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
                    {
                        int count = Convert.ToInt32(checkCmd.ExecuteScalar());
                        if (count > 0)
                        {

                            string updateSql = @"UPDATE imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK SET                                         
                                        PREP_START_DATE=:PREP_START_DATE,
                                        PREP_END_DATE=:PREP_END_DATE,
                                        CONS_ST_DATE=:CONS_ST_DATE,
                                        NOA_FINES=:NOA_FINES,
                                        JODA_FINES=:JODA_FINES,
                                        KB_FINES=:KB_FINES 		                                                                                                                                                         
                                    WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                            using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                            {
                                updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;                        
                                updateCmd.ExecuteNonQuery();
                                message = "Record updated successfully.";
                            }
                        }
                        else
                        {

                            string insertSql = @"INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                            (PILE_NO,PREP_START_DATE,PREP_END_DATE,CONS_ST_DATE,NOA_FINES,JODA_FINES,KB_FINES) 
                            values(:PILE_NO,:PREP_START_DATE,:PREP_END_DATE,:CONS_ST_DATE,:NOA_FINES,:JODA_FINES,:KB_FINES)";
                            using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                            {
                                insertCmd.Parameters.Add("PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                                insertCmd.Parameters.Add("Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                                insertCmd.Parameters.Add("EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("ConstStartDate", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("NoaFines",OracleDbType.Decimal).Value	=	input.NOA_FINES	??	(object)DBNull.Value	;
                                insertCmd.Parameters.Add("JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;                            
                                insertCmd.ExecuteNonQuery();
                            }
                        }
                    }
                }

                ViewBag.Message = "Data Saved Successfully";
                model = input;
            }            
           
            else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {

                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK  WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                model.PileNo = input.PileNo;
                                model.Source = input.Source;
                                model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                                model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                                model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                                model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                                model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                                model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);                             
                               
                            }
                        }
                    }
                }
            }

            return View(model);
        }
