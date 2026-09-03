[HttpGet]
public JsonResult GET_TLC_DAILY_REPORT(DateTime vdate)
{
    List<TLCDailyReport> list = new List<TLCDailyReport>();

    try
    {
        using (OracleConnection con =
            new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // STEP 1: Get TLC_NO from master table
            string masterQuery = @"
                SELECT TLC_NO,
                       MATURITY_LIFE,
                       TLC_SIZE
                FROM DEMO.T_TLC_MASTER
                ORDER BY TLC_NO";

            List<TLCDailyReport> masterList =
                new List<TLCDailyReport>();

            using (OracleCommand cmd =
                new OracleCommand(masterQuery, con))
            {
                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        TLCDailyReport model =
                            new TLCDailyReport();

                        model.TLC_NO = dr["TLC_NO"] == DBNull.Value
                            ? 0
                            : Convert.ToInt32(dr["TLC_NO"]);

                        model.MATURITY_LIFE =
                            dr["MATURITY_LIFE"] == DBNull.Value
                            ? 0
                            : Convert.ToInt32(dr["MATURITY_LIFE"]);

                        model.TLC_SIZE =
                            dr["TLC_SIZE"] == DBNull.Value
                            ? null
                            : dr["TLC_SIZE"].ToString();

                        masterList.Add(model);
                    }
                }
            }


            // STEP 2: Call separate function
            // for every TLC_NO
            foreach (TLCDailyReport master in masterList)
            {
                int vTrp_No = master.TLC_NO;

                List<TLCDailyReport> detailList =
                    GetTLCDetails(con, vdate, vTrp_No);

                foreach (TLCDailyReport detail in detailList)
                {
                    // Master table values
                    detail.TLC_NO = master.TLC_NO;
                    detail.MATURITY_LIFE = master.MATURITY_LIFE;
                    detail.TLC_SIZE = master.TLC_SIZE;

                    list.Add(detail);
                }
            }
        }

        return Json(new
    private List<TLCDailyReport> GetTLCDetails(
    OracleConnection con,
    DateTime vdate,
    int vTrp_No)
{
    List<TLCDailyReport> list =
        new List<TLCDailyReport>();

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
        cmd.Parameters.Add(
            ":vdate",
            OracleDbType.Date).Value = vdate;

        cmd.Parameters.Add(
            ":vTrp_No",
            OracleDbType.Int32).Value = vTrp_No;


        using (OracleDataReader dr =
            cmd.ExecuteReader())
        {
            while (dr.Read())
            {
                TLCDailyReport model =
                    new TLCDailyReport();

                model.TLC_NO =
                    dr["TLC_NO"] == DBNull.Value
                    ? 0
                    : Convert.ToInt32(dr["TLC_NO"]);

                model.TLC_ST_DATE =
                    dr["TLC_ST_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(
                        dr["TLC_ST_DATE"]);

                model.TLC_END_DATE =
                    dr["TLC_END_DATE"] == DBNull.Value
                    ? (DateTime?)null
                    : Convert.ToDateTime(
                        dr["TLC_END_DATE"]);

                model.TLC_STATUS =
                    dr["TLC_STATUS"] == DBNull.Value
                    ? null
                    : dr["TLC_STATUS"].ToString();

                model.TLC_CAMPAINE_NO =
                    dr["TLC_CAMPAINE_NO"] == DBNull.Value
                    ? null
                    : dr["TLC_CAMPAINE_NO"].ToString();

                model.CUMM_RUNNING_HR =
                    dr["CUMM_RUNNING_HR"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["CUMM_RUNNING_HR"]);

                model.CUMM_RUNNING_WT =
                    dr["CUMM_RUNNING_WT"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["CUMM_RUNNING_WT"]);

                model.TOTAL_RUNNING_HR =
                    dr["TOTAL_RUNNING_HR"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["TOTAL_RUNNING_HR"]);

                model.TOTAL_RUNNING_WT =
                    dr["TOTAL_RUNNING_WT"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["TOTAL_RUNNING_WT"]);

                model.MATURITY =
                    dr["MATURITY"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["MATURITY"]);

                model.QTY_PER_TRIP =
                    dr["QTY_PER_TRIP"] == DBNull.Value
                    ? (decimal?)null
                    : Convert.ToDecimal(
                        dr["QTY_PER_TRIP"]);

                list.Add(model);
            }
        }
    }

    return list;
}    {
            success = true,
            data = list
        }, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        }, JsonRequestBehavior.AllowGet);
    }
}
