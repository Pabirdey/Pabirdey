while (dr.Read())
                    {
                        TLCDailyReport model = new TLCDailyReport();                       
                        model.TLC_NO =dr["TLC_NO"] == DBNull.Value ? 0: Convert.ToInt32(dr["TLC_NO"]);                        
                        DateTime? tlcStartDate =dr["TLC_ST_DATE"] == DBNull.Value? (DateTime?)null: Convert.ToDateTime(dr["TLC_ST_DATE"]);                        
                        DateTime? tlcEndDate =dr["TLC_END_DATE"] == DBNull.Value? (DateTime?)null: Convert.ToDateTime(dr["TLC_END_DATE"]);                        
                        DateTime? finalDate;
                        if (tlcEndDate.HasValue)
                        {                            
                            finalDate = tlcEndDate;
                        }
                        else
                        {                         
                            finalDate = tlcStartDate;
                        }
                        model.TLC_ST_DATE = tlcStartDate;
                        model.TLC_END_DATE = tlcEndDate;                        
                        model.TLC_FINAL_DATE = finalDate;                                                
                        list.Add(model);
                    }

                    
