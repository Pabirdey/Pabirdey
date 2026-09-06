    private List<TLCDailyReport> GetTLCDetails(OracleConnection con,DateTime pdate,int vTrp_No)
        {
            List<TLCDailyReport> list = new List<TLCDailyReport>();            
            DateTime vdate = pdate.Date.AddHours(6);            
            DateTime vdateTrunc = pdate.Date;            
            DateTime vdatePrevious = pdate.Date.AddDays(-1).AddHours(6);            
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
            using (OracleCommand cmd = new OracleCommand(detailQuery, con))
            {
                cmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate;
                cmd.Parameters.Add(":vTrp_No", OracleDbType.Int32).Value = vTrp_No;
                using (OracleDataReader dr = cmd.ExecuteReader())
                {
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
                }
            }

            return list;
        }






sqlstr = "SELECT Count(t_ladle_details.FILL_STATUS) TOTAL_RUNNING_HR FROM demo.t_ladle_details "
sqlstr = sqlstr + " WHERE (LADLE_FLEND_TIME>='" & vfr_date & "' And LADLE_FLEND_TIME<='" & vdate & "') AND (TRP_NO=" & vTrp_No & ") AND (RET_FLAG='N')"
rs.Open sqlstr, con, adOpenStatic, adLockOptimistic
       If rs!TOTAL_RUNNING_HR = 0 Or IsNull(rs!TOTAL_RUNNING_HR) = True Then
            Sheets("Report").Cells(i, 3) = "RELINE"
        Else
            Sheets("Report").Cells(i, 3) = rs!TOTAL_RUNNING_HR
       End If
   rs.Close
    If Sheets("Report").Cells(i, 3) = "RELINE" Then
        Range("E" & i & ":T" & i) = ""
        ''''''''''''''
    Else
       If Sheets("Report").Cells(i, 3) = "RELINE" Then
        Sheets("Report").Cells(i, 5) = ""
        Else
        Sheets("Report").Cells(i, 5) = (Sheets("Report").Cells(i, 3) / Sheets("Report").Cells(i, 4)) * 100
       End If
