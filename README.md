public JsonResult GET_GBF_IBF_ACTUAL_REPORT(string prodDate)
{
    BFViewModel model = new BFViewModel();

    model.Furnaces = new List<GBFTOIBFPRODUCTION>();

    DateTime dt = Convert.ToDateTime(prodDate);

    string[] furnaces = { "G", "H", "I" };

    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        foreach (string furnace in furnaces)
        {
            GBFTOIBFPRODUCTION row =
                new GBFTOIBFPRODUCTION();

            row.FURNACE = furnace;

            int count = 0;

            #region CHECK PRODUCTION TRACKING RECORD

            string chkQry = @"
                    SELECT COUNT(*)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP = :PDATE
                    AND FURNACE = :FURNACE";

            using (OracleCommand chkCmd =
                new OracleCommand(chkQry, con))
            {
                chkCmd.Parameters.Add("PDATE",
                    OracleDbType.Date).Value = dt;

                chkCmd.Parameters.Add("FURNACE",
                    OracleDbType.Varchar2).Value = furnace;

                count = Convert.ToInt32(
                    chkCmd.ExecuteScalar());
            }

            #endregion

            #region IF RECORD EXISTS

            if (count > 0)
            {
                string qry = @"
                        SELECT
                            NVL(ACTUAL,0),
                            NVL(REPORTED,0),
                            NVL(BALANCE,0)
                        FROM DEMO.T_BF_PRODUCTION_TRACKING
                        WHERE TIMESTAMP = :PDATE
                        AND FURNACE = :FURNACE";

                using (OracleCommand cmd =
                    new OracleCommand(qry, con))
                {
                    cmd.Parameters.Add("PDATE",
                        OracleDbType.Date).Value = dt;

                    cmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value = furnace;

                    OracleDataReader dr =
                        cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        row.ACTUAL =
                            Convert.ToDecimal(dr[0]);

                        row.REPORTED =
                            Convert.ToDecimal(dr[1]);

                        row.BALANCE =
                            Convert.ToDecimal(dr[2]);
                    }
                }
            }

            #endregion

            #region ELSE CALCULATE LIVE DATA

            else
            {
                string actualQry = @"
                        SELECT NVL(SUM(NET_WT),0)
                        FROM DEMO.T_LADLE_DETAILS
                        WHERE LADLE_FLEND_TIME >= :FROMDATE
                        AND LADLE_FLEND_TIME < :TODATE
                        AND DESTINATION <> 'R'
                        AND FUR_NAME = :FURNACE";

                using (OracleCommand actualCmd =
                    new OracleCommand(actualQry, con))
                {
                    actualCmd.Parameters.Add("FROMDATE",
                        OracleDbType.Date).Value =
                        dt.AddHours(6);

                    actualCmd.Parameters.Add("TODATE",
                        OracleDbType.Date).Value =
                        dt.AddDays(1).AddHours(6);

                    actualCmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value =
                        furnace;

                    row.ACTUAL = Convert.ToDecimal(
                        actualCmd.ExecuteScalar());
                }

                string balQry = @"
                        SELECT
                        NVL(SUM(NVL(ACTUAL,0) -
                        NVL(REPORTED,0)),0)
                        FROM DEMO.T_BF_PRODUCTION_TRACKING
                        WHERE TIMESTAMP >=
                        TRUNC(:PDATE,'MON')
                        AND TIMESTAMP < :PDATE
                        AND FURNACE = :FURNACE";

                using (OracleCommand balCmd =
                    new OracleCommand(balQry, con))
                {
                    balCmd.Parameters.Add("PDATE",
                        OracleDbType.Date).Value = dt;

                    balCmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value =
                        furnace;

                    row.BALANCE =
                        Convert.ToDecimal(
                        balCmd.ExecuteScalar());
                }

                row.REPORTED =
                    row.ACTUAL + row.BALANCE;

                row.BALANCE =
                    row.ACTUAL -
                    row.REPORTED +
                    row.BALANCE;
            }

            #endregion

            #region TD TOTAL

            string tdQry = @"
                    SELECT
                        NVL(SUM(ACTUAL),0),
                        NVL(SUM(REPORTED),0)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP >=
                    TRUNC(:PDATE,'MON')
                    AND TIMESTAMP < :PDATE
                    AND FURNACE = :FURNACE";

            decimal prevActual = 0;
            decimal prevReported = 0;

            using (OracleCommand tdCmd =
                new OracleCommand(tdQry, con))
            {
                tdCmd.Parameters.Add("PDATE",
                    OracleDbType.Date).Value = dt;

                tdCmd.Parameters.Add("FURNACE",
                    OracleDbType.Varchar2).Value =
                    furnace;

                OracleDataReader tdDr =
                    tdCmd.ExecuteReader();

                if (tdDr.Read())
                {
                    prevActual =
                        Convert.ToDecimal(tdDr[0]);

                    prevReported =
                        Convert.ToDecimal(tdDr[1]);
                }
            }

            row.ACTUAL_TD =
                prevActual + row.ACTUAL;

            row.REPORTED_TD =
                prevReported + row.REPORTED;

            #endregion

            #region LOAD LADLE DATA

            LoadLadleData(con, dt, furnace, row);

            #endregion

            #region DISPLAY TOTAL

            model.DISPLAY_ACTUAL += row.ACTUAL;

            model.DISPLAY_REPORTED += row.REPORTED;

            model.DISPLAY_BALANCE += row.BALANCE;

            model.DISPLAY_ACTUAL_TD += row.ACTUAL_TD;

            model.DISPLAY_REPORTED_TD += row.REPORTED_TD;

            #endregion

            model.Furnaces.Add(row);
        }
    }

    return Json(model, JsonRequestBehavior.AllowGet);
}



private void LoadLadleData(
    OracleConnection con,
    DateTime dt,
    string furnace,
    GBFTOIBFPRODUCTION row)
{
    int count = 0;

    string chkQry = @"
            SELECT COUNT(*)
            FROM DEMO.T_LADLE
            WHERE DATE_TIME = :PDATE
            AND PLANT = :PLANT";

    using (OracleCommand cmd =
        new OracleCommand(chkQry, con))
    {
        cmd.Parameters.Add("PDATE",
            OracleDbType.Date).Value = dt;

        cmd.Parameters.Add("PLANT",
            OracleDbType.Varchar2).Value = furnace;

        count = Convert.ToInt32(
            cmd.ExecuteScalar());
    }

    #region IF T_LADLE RECORD EXISTS

    if (count > 0)
    {
        string qry = @"
                SELECT
                    NVL(LD1_TONS,0),
                    NVL(LD2_TONS,0),
                    NVL(LD3_TONS,0),
                    NVL(MRDTP_TONS,0),
                    NVL(NOOFTP,0),
                    NVL(LD1_TONS_ACTUAL,0),
                    NVL(LD2_TONS_ACTUAL,0),
                    NVL(LD3_TONS_ACTUAL,0),
                    NVL(MRDTP_TONS_ACTUAL,0)
                FROM DEMO.T_LADLE
                WHERE DATE_TIME = :PDATE
                AND PLANT = :PLANT";

        using (OracleCommand cmd =
            new OracleCommand(qry, con))
        {
            cmd.Parameters.Add("PDATE",
                OracleDbType.Date).Value = dt;

            cmd.Parameters.Add("PLANT",
                OracleDbType.Varchar2).Value = furnace;

            OracleDataReader dr =
                cmd.ExecuteReader();

            if (dr.Read())
            {
                row.LD1_TONS =
                    Convert.ToDecimal(dr[0]);

                row.LD2_TONS =
                    Convert.ToDecimal(dr[1]);

                row.LD3_TONS =
                    Convert.ToDecimal(dr[2]);

                row.MRDTP_TONS =
                    Convert.ToDecimal(dr[3]);

                row.NOOFTP =
                    Convert.ToDecimal(dr[4]);

                row.LD1_TONS_ACTUAL =
                    Convert.ToDecimal(dr[5]);

                row.LD2_TONS_ACTUAL =
                    Convert.ToDecimal(dr[6]);

                row.LD3_TONS_ACTUAL =
                    Convert.ToDecimal(dr[7]);

                row.MRDTP_TONS_ACTUAL =
                    Convert.ToDecimal(dr[8]);
            }
        }
    }

    #endregion

    #region ELSE CALCULATE FROM LADLE DETAILS

    else
    {
        row.LD1_TONS =
            GetDestinationTotal(con,
            dt,
            furnace,
            "LD1");

        row.LD2_TONS =
            GetDestinationTotal(con,
            dt,
            furnace,
            "LD2");

        row.LD3_TONS =
            GetDestinationTotal(con,
            dt,
            furnace,
            "LD3");

        row.MRDTP_TONS =
            GetDestinationTotal(con,
            dt,
            furnace,
            "MRD");

        row.LD1_TONS_ACTUAL =
            row.LD1_TONS;

        row.LD2_TONS_ACTUAL =
            row.LD2_TONS;

        row.LD3_TONS_ACTUAL =
            row.LD3_TONS;

        row.MRDTP_TONS_ACTUAL =
            row.MRDTP_TONS;

        row.NOOFTP =
            GetTP(con,
            dt,
            furnace);
    }

    #endregion
}



private decimal GetDestinationTotal(
    OracleConnection con,
    DateTime dt,
    string furnace,
    string destination)
{
    string qry = @"
            SELECT NVL(SUM(NET_WT),0)
            FROM DEMO.T_LADLE_DETAILS
            WHERE LADLE_FLEND_TIME >= :FROMDATE
            AND LADLE_FLEND_TIME < :TODATE
            AND DESTINATION = :DESTINATION
            AND FUR_NAME = :FURNACE";

    using (OracleCommand cmd =
        new OracleCommand(qry, con))
    {
        cmd.Parameters.Add("FROMDATE",
            OracleDbType.Date).Value =
            dt.AddHours(6);

        cmd.Parameters.Add("TODATE",
            OracleDbType.Date).Value =
            dt.AddDays(1).AddHours(6);

        cmd.Parameters.Add("DESTINATION",
            OracleDbType.Varchar2).Value =
            destination;

        cmd.Parameters.Add("FURNACE",
            OracleDbType.Varchar2).Value =
            furnace;

        return Convert.ToDecimal(
            cmd.ExecuteScalar());
    }
}



private decimal GetTP(
    OracleConnection con,
    DateTime dt,
    string furnace)
{
    string qry = @"
            SELECT NVL(SUM(FILL_STATUS),0)
            FROM DEMO.T_LADLE_DETAILS
            WHERE LADLE_FLEND_TIME >= :FROMDATE
            AND LADLE_FLEND_TIME < :TODATE
            AND TRP_NO <= 50
            AND RET_FLAG = 'N'
            AND FUR_NAME = :FURNACE";

    using (OracleCommand cmd =
        new OracleCommand(qry, con))
    {
        cmd.Parameters.Add("FROMDATE",
            OracleDbType.Date).Value =
            dt.AddHours(6);

        cmd.Parameters.Add("TODATE",
            OracleDbType.Date).Value =
            dt.AddDays(1).AddHours(6);

        cmd.Parameters.Add("FURNACE",
            OracleDbType.Varchar2).Value =
            furnace;

        return Convert.ToDecimal(
            cmd.ExecuteScalar());
    }
}
