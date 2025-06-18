 else if (!string.IsNullOrEmpty(model.PileNo) && !string.IsNullOrEmpty(model.Source))
            {                

                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + model.PileNo + "' AND SOURCE ='" + model.Source + "'";

                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                                model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                                model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                                model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) : 0;
                                model.JodaFines = reader["JODA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["JODA_FINES"]) : 0;
                                model.KBFines = reader["KB_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["KB_FINES"]) : 0;
                                model.YardFines = reader["YARD_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["YARD_FINES"]) : 0;
                             
                            }
                        }
                    }
                }
