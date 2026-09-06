private List<TLCDailyReport> GetTLCDetails(
    OracleConnection con,
    DateTime pdate,
    int vTrp_No)
{
    List<TLCDailyReport> list = new List<TLCDailyReport>();

    // =====================================================
    // DATE VARIABLES
    // =====================================================

    // Current production date at 06:00 AM
    DateTime vdate = pdate.Date.AddHours(6);

    // Current date at 00:00:00
    DateTime vdateTrunc = pdate.Date;

    // Previous day at 06:00 AM
    DateTime vdatePrevious = pdate.Date
                                .AddDays(-1)
                                .AddHours(6);


    // =====================================================
    // SQL QUERY
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


    // =====================================================
    // ORACLE COMMAND
    // =====================================================

    using (OracleCommand cmd = new OracleCommand(detailQuery, con))
    {
        cmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate;

        cmd.Parameters.Add(":vTrp_No", OracleDbType.Int32).Value = vTrp_No;


        // =================================================
        // EXECUTE QUERY
        // =================================================

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
                // YOUR REQUIRED LOGIC
                //
                // TLC_END_DATE NULL
                //      ↓
                // TLC_ST_DATE captured
                //
                // TLC_END_DATE NOT NULL
                //      ↓
                // TLC_END_DATE captured
                // =================================================

                DateTime? finalDate;

                if (tlcEndDate.HasValue)
                {
                    // TLC_END_DATE is NOT NULL
                    finalDate = tlcEndDate;
                }
                else
                {
                    // TLC_END_DATE is NULL
                    finalDate = tlcStartDate;
                }


                // =================================================
                // ASSIGN ORIGINAL DATES
                // =================================================

                model.TLC_ST_DATE = tlcStartDate;

                model.TLC_END_DATE = tlcEndDate;


                // =================================================
                // ASSIGN FINAL DATE
                // =================================================

                model.TLC_FINAL_DATE = finalDate;


                // =================================================
                // ADD TO LIST
                // =================================================

                list.Add(model);
            }
        }
    }

    return list;
}
