   private List<TLCDailyReport> GetTLCDetails(
     OracleConnection con,
     DateTime pdate,
     int vTrp_No,int vMaturity_Life)
        {
            List<TLCDailyReport> list = new List<TLCDailyReport>();
            DateTime vdate = pdate.Date.AddHours(6);            
            string detailQuery = @"
        SELECT
            a.TLC_NO,
            a.TLC_ST_DATE,
            a.TLC_END_DATE,
            a.TLC_STATUS,
            a.TLC_CAMPAINE_NO,
            a.CUMM_RUNNING_HR,
            a.CUMM_RUNNING_WT,
            a.TOTAL_RUNNING_HR,
            a.TOTAL_RUNNING_WT,
            a.MATURITY,
            a.QTY_PER_TRIP
        FROM DEMO.T_TLC_DETAILS a,
        (
            SELECT
                c.TLC_NO AS TLC_NO2,
                MAX(c.TLC_ST_DATE) AS TLC_ST_DATE2,
                MAX(c.SEQNO) AS SEQNO2
            FROM DEMO.T_TLC_DETAILS c
            WHERE c.TLC_ST_DATE < :vdate
              AND c.TLC_STATUS <> 'MID_TERM'
            GROUP BY c.TLC_NO
        ) b
        WHERE a.TLC_NO = :vTrp_No
          AND b.TLC_NO2 = :vTrp_No
          AND a.SEQNO = b.SEQNO2
        ORDER BY a.TLC_END_DATE DESC";


            using (OracleCommand cmd =
                new OracleCommand(detailQuery, con))
            {
                cmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate;

                cmd.Parameters.Add(":vTrp_No", OracleDbType.Int32).Value =
                    vTrp_No;


                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        TLCDailyReport model = new TLCDailyReport();


                        model.TLC_NO =
                            dr["TLC_NO"] == DBNull.Value
                            ? 0
                            : Convert.ToInt32(dr["TLC_NO"]);


                        DateTime? tlcStartDate =
                            dr["TLC_ST_DATE"] == DBNull.Value
                            ? (DateTime?)null
                            : Convert.ToDateTime(dr["TLC_ST_DATE"]);
                        
                        DateTime? tlcEndDate =
                            dr["TLC_END_DATE"] == DBNull.Value
                            ? (DateTime?)null
                            : Convert.ToDateTime(dr["TLC_END_DATE"]);

                        

                        DateTime? finalDate;

                        if (tlcEndDate.HasValue)
                        {
                            finalDate = tlcEndDate;
                        }
                        else
                        {
                            finalDate = tlcStartDate;
                        }
                        
                        DateTime? vfr_date = finalDate;


                        int totalRunningHr = 0;

                        if (vfr_date.HasValue)
                        {
                            string ladleQuery = @"
                        SELECT COUNT(t.FILL_STATUS)
                        FROM DEMO.T_LADLE_DETAILS t
                        WHERE t.LADLE_FLEND_TIME >= :vfr_date
                          AND t.LADLE_FLEND_TIME <= :vdate
                          AND t.TRP_NO = :vTrp_No
                          AND t.RET_FLAG = 'N'";


                            using (OracleCommand ladleCmd =
                                new OracleCommand(ladleQuery, con))
                            {
                              
                                ladleCmd.Parameters.Add(
                                    ":vfr_date",
                                    OracleDbType.Date).Value =
                                    vfr_date.Value;


                               
                                ladleCmd.Parameters.Add(
                                    ":vdate",
                                    OracleDbType.Date).Value =
                                    vdate;


                              
                                ladleCmd.Parameters.Add(
                                    ":vTrp_No",
                                    OracleDbType.Int32).Value =
                                    vTrp_No;
                                ladleCmd.Parameters.Add(
                                   ":vMaturity_Life",
                                   OracleDbType.Int32).Value =
                                   vMaturity_Life;

                                object result =
                                    ladleCmd.ExecuteScalar();


                                if (result != null &&
                                    result != DBNull.Value)
                                {
                                    totalRunningHr =
                                        Convert.ToInt32(result);
                                }
                            }
                        }


                      
                        string runningHrDisplay;
                        int maturityPerc;

                        if (totalRunningHr == 0)
                        {
                            runningHrDisplay = "RELINE";
                        }
                        else
                        {
                            runningHrDisplay =totalRunningHr.ToString();
                            maturityPerc = totalRunningHr / vMaturity_Life * 100;
                        }

                        model.TLC_ST_DATE = tlcStartDate;

                        model.TLC_END_DATE = tlcEndDate;

                        model.TLC_FINAL_DATE = finalDate; 

                        model.TLC_TOTAL_RUNNING_HR = totalRunningHr;

                        model.TLC_RUNNING_HR_DISPLAY = runningHrDisplay;
                        model.TLC_MATURITY_PERC= maturityPerc;                     

                        list.Add(model);
                    }
                }
            }

            return list;
        }
