public JsonResult GetPlantData(string prodDate)
{
    try
    {
        BFViewModel model = new BFViewModel();

        DateTime dt = DateTime.ParseExact(
            prodDate,
            "dd/MMM/yyyy",
            System.Globalization.CultureInfo.InvariantCulture
        );

        string[] furnaces = { "G", "H", "I" };

        using (OracleConnection con =
            new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            foreach (string furnace in furnaces)
            {
                /* ===================================
                   TODATE DATA
                =================================== */

                string tdQuery = @"
                SELECT
                    NVL(SUM(NOOFTP),0) NO_TP_TD,
                    NVL(SUM(LD1_TONS_ACTUAL),0) LD1_TD,
                    NVL(SUM(LD2_TONS_ACTUAL),0) LD2_TD,
                    NVL(SUM(LD3_TONS_ACTUAL),0) LD3_TD,
                    NVL(SUM(MRDTP_TONS_ACTUAL),0) MRD_TD
                FROM demo.t_ladle
                WHERE date_time >= TRUNC(:prodDate,'MON')
                AND date_time < :prodDate
                AND plant = :furnace";

                decimal vNO_TP_TD = 0;
                decimal vLD1_TD = 0;
                decimal vLD2_TD = 0;
                decimal vLD3_TD = 0;
                decimal vMRD_TD = 0;

                using (OracleCommand cmd = new OracleCommand(tdQuery, con))
                {
                    cmd.BindByName = true;

                    cmd.Parameters.Add("prodDate",
                        OracleDbType.Date).Value = dt;

                    cmd.Parameters.Add("furnace",
                        OracleDbType.Varchar2).Value = furnace;

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            vNO_TP_TD =
                                dr["NO_TP_TD"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["NO_TP_TD"]);

                            vLD1_TD =
                                dr["LD1_TD"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD1_TD"]);

                            vLD2_TD =
                                dr["LD2_TD"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD2_TD"]);

                            vLD3_TD =
                                dr["LD3_TD"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD3_TD"]);

                            vMRD_TD =
                                dr["MRD_TD"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["MRD_TD"]);
                        }
                    }
                }

                /* ===================================
                   CURRENT DAY DATA
                =================================== */

                string currentQuery = @"
                SELECT
                    DATE_TIME,
                    NVL(LD1_TONS,0) LD1_TONS,
                    NVL(LD2_TONS,0) LD2_TONS,
                    NVL(LD3_TONS,0) LD3_TONS,
                    NVL(MRDTP_TONS,0) MRDTP_TONS,
                    NVL(NOOFTP,0) NOOFTP,
                    NVL(LD1_TONS_ACTUAL,0) LD1_TONS_ACTUAL,
                    NVL(LD2_TONS_ACTUAL,0) LD2_TONS_ACTUAL,
                    NVL(LD3_TONS_ACTUAL,0) LD3_TONS_ACTUAL,
                    NVL(MRDTP_TONS_ACTUAL,0) MRDTP_TONS_ACTUAL
                FROM demo.t_ladle
                WHERE date_time = :prodDate
                AND plant = :furnace";

                bool recordFound = false;

                decimal ld1 = 0;
                decimal ld2 = 0;
                decimal ld3 = 0;
                decimal mrd = 0;

                decimal nooftp = 0;

                decimal ld1Act = 0;
                decimal ld2Act = 0;
                decimal ld3Act = 0;
                decimal mrdAct = 0;

                using (OracleCommand cmd =
                    new OracleCommand(currentQuery, con))
                {
                    cmd.BindByName = true;

                    cmd.Parameters.Add("prodDate",
                        OracleDbType.Date).Value = dt;

                    cmd.Parameters.Add("furnace",
                        OracleDbType.Varchar2).Value = furnace;

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            recordFound = true;

                            ld1 =
                                dr["LD1_TONS"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD1_TONS"]);

                            ld2 =
                                dr["LD2_TONS"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD2_TONS"]);

                            ld3 =
                                dr["LD3_TONS"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD3_TONS"]);

                            mrd =
                                dr["MRDTP_TONS"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["MRDTP_TONS"]);

                            nooftp =
                                dr["NOOFTP"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["NOOFTP"]);

                            ld1Act =
                                dr["LD1_TONS_ACTUAL"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD1_TONS_ACTUAL"]);

                            ld2Act =
                                dr["LD2_TONS_ACTUAL"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD2_TONS_ACTUAL"]);

                            ld3Act =
                                dr["LD3_TONS_ACTUAL"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["LD3_TONS_ACTUAL"]);

                            mrdAct =
                                dr["MRDTP_TONS_ACTUAL"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(dr["MRDTP_TONS_ACTUAL"]);
                        }
                    }
                }

                /* ===================================
                   IF RECORD NOT FOUND
                =================================== */

                if (!recordFound)
                {
                    string detailQuery = @"
                    SELECT
                        NVL(SUM(CASE
                            WHEN DESTINATION='LD1'
                            THEN NET_WT
                            ELSE 0 END),0) LD1,

                        NVL(SUM(CASE
                            WHEN DESTINATION='LD2'
                            THEN NET_WT
                            ELSE 0 END),0) LD2,

                        NVL(SUM(CASE
                            WHEN DESTINATION='LD3'
                            THEN NET_WT
                            ELSE 0 END),0) LD3,

                        NVL(SUM(CASE
                            WHEN DESTINATION='MRD'
                            THEN NET_WT
                            ELSE 0 END),0) MRD,

                        NVL(SUM(CASE
                            WHEN TRP_NO<=50
                            AND RET_FLAG='N'
                            THEN FILL_STATUS
                            ELSE 0 END),0) NOOFTP

                    FROM demo.t_ladle_details

                    WHERE LADLE_FLEND_TIME >= :fromDate
                    AND LADLE_FLEND_TIME < :toDate
                    AND fur_name = :furnace";

                    using (OracleCommand cmd =
                        new OracleCommand(detailQuery, con))
                    {
                        cmd.BindByName = true;

                        cmd.Parameters.Add("fromDate",
                            OracleDbType.Date).Value =
                            dt.AddHours(6);

                        cmd.Parameters.Add("toDate",
                            OracleDbType.Date).Value =
                            dt.AddDays(1).AddHours(6);

                        cmd.Parameters.Add("furnace",
                            OracleDbType.Varchar2).Value = furnace;

                        using (OracleDataReader dr = cmd.ExecuteReader())
                        {
                            if (dr.Read())
                            {
                                ld1 =
                                    dr["LD1"] == DBNull.Value
                                    ? 0
                                    : Convert.ToDecimal(dr["LD1"]);

                                ld2 =
                                    dr["LD2"] == DBNull.Value
                                    ? 0
                                    : Convert.ToDecimal(dr["LD2"]);

                                ld3 =
                                    dr["LD3"] == DBNull.Value
                                    ? 0
                                    : Convert.ToDecimal(dr["LD3"]);

                                mrd =
                                    dr["MRD"] == DBNull.Value
                                    ? 0
                                    : Convert.ToDecimal(dr["MRD"]);

                                nooftp =
                                    dr["NOOFTP"] == DBNull.Value
                                    ? 0
                                    : Convert.ToDecimal(dr["NOOFTP"]);

                                ld1Act = ld1;
                                ld2Act = ld2;
                                ld3Act = ld3;
                                mrdAct = mrd;
                            }
                        }
                    }
                }

                /* ===================================
                   SWITCH CASE
                =================================== */

                switch (furnace)
                {
                    case "G":

                        model.LD1_TONS_G = ld1;
                        model.LD2_TONS_G = ld2;
                        model.LD3_TONS_G = ld3;
                        model.MRDTP_TONS_G = mrd;

                        model.NOOFTP_G = nooftp;

                        model.LD1_TONS_ACTUAL_G = ld1Act;
                        model.LD2_TONS_ACTUAL_G = ld2Act;
                        model.LD3_TONS_ACTUAL_G = ld3Act;
                        model.MRDTP_TONS_ACTUAL_G = mrdAct;

                        model.LD1_TONS_ACTUAL_TD_G =
                            vLD1_TD + ld1Act;

                        model.LD2_TONS_ACTUAL_TD_G =
                            vLD2_TD + ld2Act;

                        model.LD3_TONS_ACTUAL_TD_G =
                            vLD3_TD + ld3Act;

                        model.MRD_TONS_ACTUAL_TD_G =
                            vMRD_TD + mrdAct;

                        model.NO_TP_TD_G =
                            vNO_TP_TD + nooftp;

                        break;

                    case "H":

                        model.LD1_TONS_H = ld1;
                        model.LD2_TONS_H = ld2;
                        model.LD3_TONS_H = ld3;
                        model.MRDTP_TONS_H = mrd;

                        model.NOOFTP_H = nooftp;

                        model.LD1_TONS_ACTUAL_H = ld1Act;
                        model.LD2_TONS_ACTUAL_H = ld2Act;
                        model.LD3_TONS_ACTUAL_H = ld3Act;
                        model.MRDTP_TONS_ACTUAL_H = mrdAct;

                        model.LD1_TONS_ACTUAL_TD_H =
                            vLD1_TD + ld1Act;

                        model.LD2_TONS_ACTUAL_TD_H =
                            vLD2_TD + ld2Act;

                        model.LD3_TONS_ACTUAL_TD_H =
                            vLD3_TD + ld3Act;

                        model.MRD_TONS_ACTUAL_TD_H =
                            vMRD_TD + mrdAct;

                        model.NO_TP_TD_H =
                            vNO_TP_TD + nooftp;

                        break;

                    case "I":

                        model.LD1_TONS_I = ld1;
                        model.LD2_TONS_I = ld2;
                        model.LD3_TONS_I = ld3;
                        model.MRDTP_TONS_I = mrd;

                        model.NOOFTP_I = nooftp;

                        model.LD1_TONS_ACTUAL_I = ld1Act;
                        model.LD2_TONS_ACTUAL_I = ld2Act;
                        model.LD3_TONS_ACTUAL_I = ld3Act;
                        model.MRDTP_TONS_ACTUAL_I = mrdAct;

                        model.LD1_TONS_ACTUAL_TD_I =
                            vLD1_TD + ld1Act;

                        model.LD2_TONS_ACTUAL_TD_I =
                            vLD2_TD + ld2Act;

                        model.LD3_TONS_ACTUAL_TD_I =
                            vLD3_TD + ld3Act;

                        model.MRD_TONS_ACTUAL_TD_I =
                            vMRD_TD + mrdAct;

                        model.NO_TP_TD_I =
                            vNO_TP_TD + nooftp;

                        break;
                }
            }
        }

        return Json(new
        {
            status = true,
            data = model
        }, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new
        {
            status = false,
            message = ex.Message
        }, JsonRequestBehavior.AllowGet);
    }
}
