	select COUNT(*) INTO V_TEMP from DEMO.T_LADLE where DATE_TIME=:ctl_blk.ctl_date_time_prod and PLANT ='G'; 
		
		IF V_TEMP>0 THEN 	
			
					
 				select DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME,:BLK_CONTROL.LD1_TONS_G,:BLK_CONTROL.LD2_TONS_G,:BLK_CONTROL.LD3_TONS_G,:BLK_CONTROL.MRDTP_TONS_G,:BLK_CONTROL.NOOFTP_G,
		                     :BLK_CONTROL.LD1_TONS_ACTUAL_G,:BLK_CONTROL.LD2_TONS_ACTUAL_G,:BLK_CONTROL.LD3_TONS_ACTUAL_G,:BLK_CONTROL.MRDTP_TONS_ACTUAL_G		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='G';

		                
		Else

				SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					 AND DESTINATION='LD1' and fur_name='G';	
					:BLK_CONTROL.LD1_TONS_ACTUAL_G:=:BLK_CONTROL.LD1_TONS_G;
					
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD2' and fur_name ='G';	
					:BLK_CONTROL.LD2_TONS_ACTUAL_G:=:BLK_CONTROL.LD2_TONS_G;
						
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD3' and fur_name ='G';	
					:BLK_CONTROL.LD3_TONS_ACTUAL_G:=:BLK_CONTROL.LD3_TONS_G;
					
						SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.MRDTP_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='MRD' and fur_name ='G';	
				:BLK_CONTROL.MRDTP_TONS_ACTUAL_G:=:BLK_CONTROL.MRDTP_TONS_G;
				
				SELECT NVL(SUM(FILL_STATUS),0) INTO :BLK_CONTROL.NOOFTP_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
							AND  TRP_NO<=50 and fur_name ='G' and ret_flag='N';
							
		End If;
   public JsonResult GetGTOIBFReportData(string fDate)
        {
            List<BF_Production> list = new List<BF_Production>();
            string[] furnaces = { "G", "H", "I" };
            try 
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    foreach (var furnace in furnaces)
                    {
                        BF_Production row = new BF_Production();

                        decimal ACTUAL = 0, REPORTED = 0, BALANCE = 0;
                        decimal ACTUAL_TD = 0, REPORTED_TD = 0;
                        decimal vActual_TD = 0, vReported_TD = 0;

                        try 
                        {                            
                            string countQuery = @"SELECT COUNT(*) 
                                          FROM DEMO.T_BF_PRODUCTION_TRACKING 
                                          WHERE TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') 
                                          AND FURNACE = :FURNACE";

                            int count = 0;

                            using (OracleCommand cmd = new OracleCommand(countQuery, con))
                            {
                                cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                count = Convert.ToInt32(cmd.ExecuteScalar());
                            }
                            if (count > 0)
                            {
                                string Sql1 = @"SELECT a.FURNACE,a.ACTUAL AS ACT_ONDT,a.REPORTED AS REPORT_ONDT,a.BALANCE,(SELECT SUM(b.ACTUAL) FROM DEMO.T_BF_PRODUCTION_TRACKING b  WHERE b.FURNACE = a.FURNACE  AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')  AND b.TIMESTAMP <= a.TIMESTAMP) AS ACT_TODT,(SELECT SUM(b.REPORTED) FROM DEMO.T_BF_PRODUCTION_TRACKING b WHERE b.FURNACE = a.FURNACE AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP <= a.TIMESTAMP) AS REPORT_TODT FROM DEMO.T_BF_PRODUCTION_TRACKING a WHERE a.TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY') AND FURNACE = :FURNACE";
                                using (OracleCommand cmd = new OracleCommand(Sql1, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                    using (var dr = cmd.ExecuteReader())
                                    {
                                        if (dr.Read())
                                        {
                                            ACTUAL = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);
                                            REPORTED = dr["REPORT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_ONDT"]);
                                            BALANCE = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);
                                            ACTUAL_TD = dr["ACT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT"]);
                                            REPORTED_TD = dr["REPORT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT"]);
                                        }
                                    }
                                }
                            }
                            else
                            {
                                string Sql1 = @"SELECT NVL(SUM(NET_WT),0) FROM DEMO.T_LADLE_DETAILS WHERE LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY')+6/24 AND LADLE_FLEND_TIME < TO_DATE(:FDate,'DD/MM/YYYY')+1+6/24 AND DESTINATION <> 'R'  AND FUR_NAME = :FURNACE";
                                using (OracleCommand cmd = new OracleCommand(Sql1, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                    ACTUAL = Convert.ToDecimal(cmd.ExecuteScalar());
                                }

                                string Sql2 = @"SELECT NVL(SUM(ACTUAL),0) - NVL(SUM(REPORTED),0) FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND TIMESTAMP < TO_DATE(:FDate,'DD/MM/YYYY') AND FURNACE = :FURNACE";
                                using (OracleCommand cmd = new OracleCommand(Sql2, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                    BALANCE = Convert.ToDecimal(cmd.ExecuteScalar());
                                }

                                REPORTED = ACTUAL + BALANCE;

                                string Sql3 = @"SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0) FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND TIMESTAMP < TO_DATE(:FDate,'DD/MM/YYYY') AND FURNACE = :FURNACE";
                                using (OracleCommand cmd = new OracleCommand(Sql3, con))
                                {
                                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                                    cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                                    using (var dr = cmd.ExecuteReader())
                                    {
                                        if (dr.Read())
                                        {
                                            vActual_TD = dr.IsDBNull(0) ? 0 : dr.GetDecimal(0);
                                            vReported_TD = dr.IsDBNull(1) ? 0 : dr.GetDecimal(1);
                                        }
                                    }
                                }

                                ACTUAL_TD = vActual_TD + ACTUAL;
                                REPORTED_TD = vReported_TD + REPORTED;
                            }
                        }
                        catch (Exception ex) 
                        {                            
                            row.FURNACE = furnace;
                            row.ACT_ONDT = 0;
                            row.REPORT_ONDT = 0;
                            row.BALANCE = 0;
                            row.ACT_TODT = null;
                            row.REPORT_TODT = null;                            
                            System.Diagnostics.Debug.WriteLine("Error for Furnace " + furnace + ": " + ex.Message);
                            list.Add(row);
                            continue;
                        }                        
                        row.FURNACE = furnace;
                        row.ACT_ONDT = ACTUAL;
                        row.REPORT_ONDT = REPORTED;
                        row.BALANCE = BALANCE;
                        row.ACT_TODT = ACTUAL_TD == 0 ? (decimal?)null : ACTUAL_TD;
                        row.REPORT_TODT = REPORTED_TD == 0 ? (decimal?)null : REPORTED_TD;
                        list.Add(row);
                    }
                }
            }
            catch (Exception ex) 
            {
                return Json(new
                {
                    success = false,
                    message = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
