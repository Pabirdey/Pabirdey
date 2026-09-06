private List<TLCDailyReport> GetTLCDetails(
    OracleConnection con,
    DateTime pdate,
    int vTrp_No)
{
    List<TLCDailyReport> list = new List<TLCDailyReport>();

    // =====================================================
    // PRODUCTION DATE
    // =====================================================

    // vdate = pdate at 06:00 AM
    DateTime vdate = pdate.Date.AddHours(6);


    // =====================================================
    // GET TLC DETAILS
    // =====================================================

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


                // =================================================
                // TLC NO
                // =================================================

                model.TLC_NO =
                    dr["TLC_NO"] == DBNull.Value
                    ? 0
                    : Convert.ToInt32(dr["TLC_NO"]);


                // =================================================
                // TLC START DATE
                // =================================================

                DateTime? tlcStartDate =
                    dr["TLC_ST_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(dr["TLC_ST_DATE"]);


                // =================================================
                // TLC END DATE
                // =================================================

                DateTime? tlcEndDate =
                    dr["TLC_END_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(dr["TLC_END_DATE"]);


                // =================================================
                // FINAL DATE
                //
                // END DATE available -> END DATE
                // END DATE NULL      -> START DATE
                // =================================================

                DateTime? finalDate;

                if (tlcEndDate.HasValue)
                {
                    finalDate = tlcEndDate;
                }
                else
                {
                    finalDate = tlcStartDate;
                }


                // =================================================
                // vfr_date = TLC_FINAL_DATE
                // =================================================

                DateTime? vfr_date = finalDate;


                // =================================================
                // GET TOTAL RUNNING HR
                //
                // VBA:
                //
                // LADLE_FLEND_TIME >= vfr_date
                // LADLE_FLEND_TIME <= vdate
                // TRP_NO = vTrp_No
                // RET_FLAG = 'N'
                // =================================================

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
                        // vfr_date = TLC_FINAL_DATE
                        ladleCmd.Parameters.Add(
                            ":vfr_date",
                            OracleDbType.Date).Value =
                            vfr_date.Value;


                        // vdate = pdate 06:00 AM
                        ladleCmd.Parameters.Add(
                            ":vdate",
                            OracleDbType.Date).Value =
                            vdate;


                        // vTrp_No = Trp argument
                        ladleCmd.Parameters.Add(
                            ":vTrp_No",
                            OracleDbType.Int32).Value =
                            vTrp_No;


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


                // =================================================
                // RELINE LOGIC
                //
                // VBA:
                //
                // If TOTAL_RUNNING_HR = 0
                //     "RELINE"
                // Else
                //     TOTAL_RUNNING_HR
                // =================================================

                string runningHrDisplay;

                if (totalRunningHr == 0)
                {
                    runningHrDisplay = "RELINE";
                }
                else
                {
                    runningHrDisplay =
                        totalRunningHr.ToString();
                }


                // =================================================
                // ASSIGN MODEL
                // =================================================

                model.TLC_ST_DATE = tlcStartDate;

                model.TLC_END_DATE = tlcEndDate;

                model.TLC_FINAL_DATE = finalDate;

                model.TOTAL_RUNNING_HR = totalRunningHr;

                model.RUNNING_HR_DISPLAY = runningHrDisplay;


                // =================================================
                // ADD LIST
                // =================================================

                list.Add(model);
            }
        }
    }

    return list;
}
