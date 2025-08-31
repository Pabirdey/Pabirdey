[HttpPost]
        public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
        {
            RmbbPile model = new RmbbPile();
            string message = "";
            bool recordFound = false;
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {

                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();


                    string checkSql = "SELECT COUNT(*) FROM Test.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
                    {
                        int count = Convert.ToInt32(checkCmd.ExecuteScalar());
                        if (count > 0)
                        {

                            string updateSql = @"UPDATE Test.T_PILE_RAWMAT_QUANTITY_NEW SET                                         
                                        PREP_START_DATE=:PREP_START_DATE,
                                        PREP_END_DATE=:PREP_END_DATE,
                                        CONS_ST_DATE=:CONS_ST_DATE,
                                        NOA_FINES=:NOA_FINES,
                                        JODA_FINES=:JODA_FINES,
                                        KB_FINES=:KB_FINES                                                                                                                                                          
                                    WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                            using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                            {
                                updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value; 
                                updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                                updateCmd.ExecuteNonQuery();
                                message = "Record Updated successfully!";
                            }
                        }
                        else
                        {

                            string insertSql = @"INSERT INTO Test.T_PILE_RAWMAT_QUANTITY_NEW
                            (PILE_NO,SOURCE,PREP_START_DATE,PREP_END_DATE,CONS_ST_DATE,NOA_FINES,
                            JODA_FINES,KB_FINES
                            values(:PILE_NO,:SOURCE,:PREP_START_DATE,:PREP_END_DATE,:CONS_ST_DATE,:NOA_FINES,
                            :JODA_FINES,:KB_FINES);
                            using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                            {
                                insertCmd.Parameters.Add("PILE_NO", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                                insertCmd.Parameters.Add("SOURCE", OracleDbType.Varchar2).Value = input.Source ?? "";                                
                                insertCmd.Parameters.Add("PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value; 
                                insertCmd.Parameters.Add("PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                                insertCmd.Parameters.Add("KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;                          
                                insertCmd.ExecuteNonQuery();
                            }
                        }
                    }
                }

                ViewBag.Message = "Data Inserted Successfully!";
                model = input;
            }

            else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {                
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();
                    string query = "SELECT * FROM Test.T_PILE_RAWMAT_QUANTITY_NEW  WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                recordFound = true;
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
                if (!recordFound)
                {
                    ViewBag.Message = "No record exists for the given Pile No and Source.";
                    model = new RmbbPile
                    {
                        PileNo = input.PileNo,
                        Source = input.Source
                    };
                               
                }
               
            }

           return View(model);
           //return View(recordFound ? model : input);

        }

  	Select  SUM(LD_Sludge), SUM(Mill_Scale),  SUM(Flue_Dust), SUM(Esp_Dust), SUM(Kiln_Dust), SUM(Gcp_Sludge), SUM(Lime_Fines), SUM(Wrp_MET), SUM(LD_Slag_Fines),SUM(MILL_SLUDGE)
									into vLD_Sludge_Cons, vMill_Scale_Cons, vFlue_Dust_Cons, vEsp_Dust_Cons, vKILN_DUST_Cons, vGcp_Sludge_Cons, vLIME_FINES_cons, vWRP_cons, vLD_SLAG_FINES_cons ,vMILL_SLUDGE_Cons from
								(
								Select vPSW1*Avg(LD_Sludge)/100 LD_Sludge,vPSW1*Avg(Mill_Scale)/100 Mill_Scale,vPSW1*Avg(Flue_Dust)/100 Flue_Dust,vPSW1*Avg(Esp_Dust)/100 Esp_Dust,vPSW1*Avg(Kiln_Dust)/100 Kiln_Dust,vPSW1*Avg(Gcp_Sludge)/100 Gcp_Sludge,vPSW1*Avg(Lime_Fines)/100 Lime_Fines,vPSW1*Avg(Wrp_MET)/100 Wrp_MET,vPSW1*Avg(LD_Slag_Fines)/100 LD_Slag_Fines,vPSW1*Avg(MILL_SLUDGE)/100  MILL_SLUDGE   
						            from T_PSW_DAILY where trim(SOURCE)='RMBB_KNR' and TIMESTAMP>=trunc(vPrep_End_Date)-200 and BLEND_NO=:BLK_PSW.LST_BL1
						    Union
						    	Select vPSW2*Avg(LD_Sludge)/100 LD_Sludge,vPSW2*Avg(Mill_Scale)/100 Mill_Scale,vPSW2*Avg(Flue_Dust)/100 Flue_Dust,vPSW2*Avg(Esp_Dust)/100 Esp_Dust,vPSW2*Avg(Kiln_Dust)/100 Kiln_Dust,vPSW2*Avg(Gcp_Sludge)/100 Gcp_Sludge,vPSW2*Avg(Lime_Fines)/100 Lime_Fines,vPSW2*Avg(Wrp_MET)/100 Wrp_MET,vPSW2*Avg(LD_Slag_Fines)/100 LD_Slag_Fines ,vPSW2*Avg(MILL_SLUDGE)/100 MILL_SLUDGE 
						            from T_PSW_DAILY where trim(SOURCE)='RMBB_KNR' and TIMESTAMP>=trunc(vPrep_End_Date)-200 and BLEND_NO=:BLK_PSW.LST_BL2
						    );
							
