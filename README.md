 [HttpPost]
        public ActionResult RawMaterialEntry(RawMaterialQuantity input,string SaveRawMaterial)
        {
            RawMaterialQuantity model = new RawMaterialQuantity()
            {
                Source = input.Source,
                PileNo = input.PileNo

            };
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {
                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();

                    using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;
                        cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                        cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                        cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? 0;
                        cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? 0;
                        cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = input.KBFines ?? 0;
                        cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = input.YardFines ?? 0;

                        cmd.ExecuteNonQuery();
                    }
                }

                ViewBag.Message = "Data Saved Successfully";
            }
           else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {

                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
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
                           
                            }
                        }
                    }
                }
            }

            return View(model);
        }
