private List<TLCDailyReport> GetTLCDetails(
    OracleConnection con,
    DateTime pdate,
    int vTrp_No)
{
    List<TLCDailyReport> list = new List<TLCDailyReport>();

    // =====================================================
    // 1. PRODUCTION DATE
    // =====================================================

    // pdate at 06:00 AM
    DateTime vdate = pdate.Date.AddHours(6);

    // pdate at 00:00:00
    DateTime vdateTrunc = pdate.Date;

    // Previous day at 06:00 AM
    DateTime vdatePrevious = pdate.Date.AddDays(-1).AddHours(6);


    // =====================================================
    // 2. GET TLC DETAILS
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


    using (OracleCommand cmd = new OracleCommand(detailQuery, con))
    {
        cmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate;
        cmd.Parameters.Add(":vTrp_No", OracleDbType.Int32).Value = vTrp_No;


        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            while (dr.Read())
            {
                TLCDailyReport model = new TLCDailyReport();


                // =================================================
                // 3. TLC NO
                // =================================================

                model.TLC_NO =
                    dr["TLC_NO"] == DBNull.Value
                    ? 0
                    : Convert.ToInt32(dr["TLC_NO"]);


                // =================================================
                // 4. TLC START DATE
                // =================================================

                DateTime? tlcStartDate =
                    dr["TLC_ST_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(dr["TLC_ST_DATE"]);


                // =================================================
                // 5. TLC END DATE
                // =================================================

                DateTime? tlcEndDate =
                    dr["TLC_END_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(dr["TLC_END_DATE"]);


                // =================================================
                // 6. FINAL DATE
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
                // 7. FINAL DATE TRUNC
                //
                // Example:
                // 06-Sep-2026 14:30:20
                //
                // becomes:
                // 06-Sep-2026 00:00:00
                // =================================================

                DateTime? finalDateTrunc;

                if (finalDate.HasValue)
                {
                    finalDateTrunc = finalDate.Value.Date;
                }
                else
                {
                    finalDateTrunc = null;
                }


                // =================================================
                // 8. vfr_date
                //
                // finalDateTrunc + 6 hours
                //
                // Example:
                // finalDateTrunc = 06-Sep-2026 00:00
                //
                // vfr_date = 06-Sep-2026 06:00
                // =================================================

                DateTime? vfr_date;

                if (finalDateTrunc.HasValue)
                {
                    vfr_date = finalDateTrunc.Value.AddHours(6);
                }
                else
                {
                    vfr_date = null;
                }


                // =================================================
                // 9. vdate
                //
                // vfr_date + 1 day
                //
                // Example:
                // vfr_date = 06-Sep-2026 06:00
                //
                // vdate = 07-Sep-2026 06:00
                // =================================================

                DateTime? ladleToDate;

                if (vfr_date.HasValue)
                {
                    ladleToDate = vfr_date.Value.AddDays(1);
                }
                else
                {
                    ladleToDate = null;
                }


                // =================================================
                // 10. GET TOTAL RUNNING HR
                //
                // Old VBA:
                //
                // SELECT Count(t_ladle_details.FILL_STATUS)
                // FROM demo.t_ladle_details
                // WHERE LADLE_FLEND_TIME >= vfr_date
                // AND LADLE_FLEND_TIME <= vdate
                // AND TRP_NO = vTrp_No
                // AND RET_FLAG = 'N'
                // =================================================

                int totalRunningHr = 0;

                if (vfr_date.HasValue && ladleToDate.HasValue)
                {
                    string ladleQuery = @"
                        SELECT COUNT(t.FILL_STATUS) AS TOTAL_RUNNING_HR
                        FROM DEMO.T_LADLE_DETAILS t
                        WHERE t.LADLE_FLEND_TIME >= :vfr_date
                          AND t.LADLE_FLEND_TIME <= :vdate
                          AND t.TRP_NO = :vTrp_No
                          AND t.RET_FLAG = 'N'";


                    using (OracleCommand ladleCmd =
                        new OracleCommand(ladleQuery, con))
                    {
                        ladleCmd.Parameters.Add(":vfr_date",
                            OracleDbType.Date).Value = vfr_date.Value;

                        ladleCmd.Parameters.Add(":vdate",
                            OracleDbType.Date).Value = ladleToDate.Value;

                        ladleCmd.Parameters.Add(":vTrp_No",
                            OracleDbType.Int32).Value = vTrp_No;


                        object result = ladleCmd.ExecuteScalar();

                        if (result != null && result != DBNull.Value)
                        {
                            totalRunningHr = Convert.ToInt32(result);
                        }
                    }
                }


                // =================================================
                // 11. ASSIGN MODEL VALUES
                // =================================================

                model.TLC_ST_DATE = tlcStartDate;

                model.TLC_END_DATE = tlcEndDate;

                model.TLC_FINAL_DATE = finalDate;

                model.TLC_FINAL_DATE_TRUNC = finalDateTrunc;

                model.TOTAL_RUNNING_HR = totalRunningHr;


                // =================================================
                // 12. ADD TO LIST
                // =================================================

                list.Add(model);
            }
        }
    }

    return list;
}
