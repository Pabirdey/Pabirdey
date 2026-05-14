// Models/BFProductionModel.cs

namespace YourProject.Models
{
    public class BFProductionModel
    {
        public DateTime PROD_DATE { get; set; }

        // =======================
        // G FURNACE
        // =======================

        public decimal? TXT_ACTUAL_G { get; set; }
        public decimal? TXT_RPT_G { get; set; }
        public decimal? TXT_BAL_G { get; set; }

        public decimal? TXT_ACTUAL_G_TD { get; set; }
        public decimal? TXT_RPT_G_TD { get; set; }

        // =======================
        // H FURNACE
        // =======================

        public decimal? TXT_ACTUAL_H { get; set; }
        public decimal? TXT_RPT_H { get; set; }
        public decimal? TXT_BAL_H { get; set; }

        public decimal? TXT_ACTUAL_H_TD { get; set; }
        public decimal? TXT_RPT_H_TD { get; set; }

        // =======================
        // I FURNACE
        // =======================

        public decimal? TXT_ACTUAL_I { get; set; }
        public decimal? TXT_RPT_I { get; set; }
        public decimal? TXT_BAL_I { get; set; }

        public decimal? TXT_ACTUAL_I_TD { get; set; }
        public decimal? TXT_RPT_I_TD { get; set; }

        // =======================
        // DISPLAY TOTAL
        // =======================

        public decimal? DISPLAY_ACT_I { get; set; }
        public decimal? DISPLAY_RPT_I { get; set; }
        public decimal? DISPLAY_BAL_I { get; set; }

        public decimal? DISPLAY_ACT_I_TD { get; set; }
        public decimal? DISPLAY_RPT_I_TD { get; set; }
    }
}


// CONTROLLER

using Oracle.ManagedDataAccess.Client;
using System;
using System.Web.Mvc;
using YourProject.Models;

public class HomeController : Controller
{
    public JsonResult GetBFProductionTracking(DateTime ctl_date_time_prod)
    {
        BFProductionModel obj = new BFProductionModel();

        decimal V_TEMP = 0;

        decimal vActual_TD = 0;
        decimal vReported_TD = 0;

        using (OracleConnection con =
            new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // =========================================================
            // G FURNACE
            // =========================================================

            string q1 = @"SELECT COUNT(*)
                          FROM DEMO.T_BF_PRODUCTION_TRACKING
                          WHERE TIMESTAMP=:P_DATE
                          AND FURNACE='G'";

            using (OracleCommand cmd = new OracleCommand(q1, con))
            {
                cmd.Parameters.Add("P_DATE",
                    OracleDbType.Date).Value = ctl_date_time_prod;

                V_TEMP = Convert.ToDecimal(cmd.ExecuteScalar());
            }

            if (V_TEMP > 0)
            {
                string q2 = @"SELECT NVL(ACTUAL,0),
                                     NVL(REPORTED,0),
                                     NVL(BALANCE,0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP=:P_DATE
                              AND FURNACE='G'";

                using (OracleCommand cmd = new OracleCommand(q2, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    OracleDataReader dr = cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        obj.TXT_ACTUAL_G =
                            Convert.ToDecimal(dr[0]);

                        obj.TXT_RPT_G =
                            Convert.ToDecimal(dr[1]);

                        obj.TXT_BAL_G =
                            Convert.ToDecimal(dr[2]);
                    }
                }

                string q3 = @"SELECT NVL(SUM(ACTUAL),0),
                                     NVL(SUM(REPORTED),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP>=TRUNC(:P_DATE,'MON')
                              AND TIMESTAMP<=:P_DATE
                              AND FURNACE='G'";

                using (OracleCommand cmd = new OracleCommand(q3, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    OracleDataReader dr = cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        obj.TXT_ACTUAL_G_TD =
                            Convert.ToDecimal(dr[0]);

                        obj.TXT_RPT_G_TD =
                            Convert.ToDecimal(dr[1]);
                    }
                }
            }
            else
            {
                string q4 = @"SELECT NVL(SUM(NET_WT),0)
                              FROM demo.t_ladle_details
                              WHERE LADLE_FLEND_TIME>=:P_DATE+6/24
                              AND LADLE_FLEND_TIME<:P_DATE+1+6/24
                              AND DESTINATION<>'R'
                              AND fur_name='G'";

                using (OracleCommand cmd = new OracleCommand(q4, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    obj.TXT_ACTUAL_G =
                        Convert.ToDecimal(cmd.ExecuteScalar());
                }

                string q5 = @"SELECT NVL(SUM(NVL(ACTUAL,0))-
                                         SUM(NVL(REPORTED,0)),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP>=TRUNC(:P_DATE,'MON')
                              AND TIMESTAMP<:P_DATE
                              AND FURNACE='G'";

                using (OracleCommand cmd = new OracleCommand(q5, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    obj.TXT_BAL_G =
                        Convert.ToDecimal(cmd.ExecuteScalar());
                }

                obj.TXT_RPT_G =
                    obj.TXT_ACTUAL_G + obj.TXT_BAL_G;

                obj.TXT_BAL_G =
                    obj.TXT_ACTUAL_G -
                    obj.TXT_RPT_G +
                    obj.TXT_BAL_G;

                string q6 = @"SELECT NVL(SUM(ACTUAL),0),
                                     NVL(SUM(REPORTED),0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP>=TRUNC(:P_DATE,'MON')
                              AND TIMESTAMP<:P_DATE
                              AND FURNACE='G'";

                using (OracleCommand cmd = new OracleCommand(q6, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    OracleDataReader dr = cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        vActual_TD =
                            Convert.ToDecimal(dr[0]);

                        vReported_TD =
                            Convert.ToDecimal(dr[1]);
                    }
                }

                obj.TXT_ACTUAL_G_TD =
                    vActual_TD + obj.TXT_ACTUAL_G;

                obj.TXT_RPT_G_TD =
                    vReported_TD + obj.TXT_RPT_G;
            }

            // =========================================================
            // H FURNACE
            // =========================================================

            V_TEMP = 0;

            string h1 = @"SELECT COUNT(*)
                          FROM DEMO.T_BF_PRODUCTION_TRACKING
                          WHERE TIMESTAMP=:P_DATE
                          AND FURNACE='H'";

            using (OracleCommand cmd = new OracleCommand(h1, con))
            {
                cmd.Parameters.Add("P_DATE",
                    OracleDbType.Date).Value = ctl_date_time_prod;

                V_TEMP = Convert.ToDecimal(cmd.ExecuteScalar());
            }

            if (V_TEMP > 0)
            {
                string h2 = @"SELECT NVL(ACTUAL,0),
                                     NVL(REPORTED,0),
                                     NVL(BALANCE,0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP=:P_DATE
                              AND FURNACE='H'";

                using (OracleCommand cmd = new OracleCommand(h2, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    OracleDataReader dr = cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        obj.TXT_ACTUAL_H =
                            Convert.ToDecimal(dr[0]);

                        obj.TXT_RPT_H =
                            Convert.ToDecimal(dr[1]);

                        obj.TXT_BAL_H =
                            Convert.ToDecimal(dr[2]);
                    }
                }
            }
            else
            {
                string h3 = @"SELECT NVL(SUM(NET_WT),0)
                              FROM demo.t_ladle_details
                              WHERE LADLE_FLEND_TIME>=:P_DATE+6/24
                              AND LADLE_FLEND_TIME<:P_DATE+1+6/24
                              AND DESTINATION<>'R'
                              AND fur_name='H'";

                using (OracleCommand cmd = new OracleCommand(h3, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    obj.TXT_ACTUAL_H =
                        Convert.ToDecimal(cmd.ExecuteScalar());
                }

                obj.TXT_RPT_H = obj.TXT_ACTUAL_H;
                obj.TXT_BAL_H = 0;
            }

            // =========================================================
            // I FURNACE
            // =========================================================

            V_TEMP = 0;

            string i1 = @"SELECT COUNT(*)
                          FROM DEMO.T_BF_PRODUCTION_TRACKING
                          WHERE TIMESTAMP=:P_DATE
                          AND FURNACE='I'";

            using (OracleCommand cmd = new OracleCommand(i1, con))
            {
                cmd.Parameters.Add("P_DATE",
                    OracleDbType.Date).Value = ctl_date_time_prod;

                V_TEMP = Convert.ToDecimal(cmd.ExecuteScalar());
            }

            if (V_TEMP > 0)
            {
                string i2 = @"SELECT NVL(ACTUAL,0),
                                     NVL(REPORTED,0),
                                     NVL(BALANCE,0)
                              FROM DEMO.T_BF_PRODUCTION_TRACKING
                              WHERE TIMESTAMP=:P_DATE
                              AND FURNACE='I'";

                using (OracleCommand cmd = new OracleCommand(i2, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    OracleDataReader dr = cmd.ExecuteReader();

                    if (dr.Read())
                    {
                        obj.TXT_ACTUAL_I =
                            Convert.ToDecimal(dr[0]);

                        obj.TXT_RPT_I =
                            Convert.ToDecimal(dr[1]);

                        obj.TXT_BAL_I =
                            Convert.ToDecimal(dr[2]);
                    }
                }
            }
            else
            {
                string i3 = @"SELECT NVL(SUM(NET_WT),0)
                              FROM demo.t_ladle_details
                              WHERE LADLE_FLEND_TIME>=:P_DATE+6/24
                              AND LADLE_FLEND_TIME<:P_DATE+1+6/24
                              AND DESTINATION<>'R'
                              AND fur_name='I'";

                using (OracleCommand cmd = new OracleCommand(i3, con))
                {
                    cmd.Parameters.Add("P_DATE",
                        OracleDbType.Date).Value = ctl_date_time_prod;

                    obj.TXT_ACTUAL_I =
                        Convert.ToDecimal(cmd.ExecuteScalar());
                }

                obj.TXT_RPT_I = obj.TXT_ACTUAL_I;
                obj.TXT_BAL_I = 0;
            }

            // =========================================================
            // TOTAL
            // =========================================================

            obj.DISPLAY_ACT_I =
                (obj.TXT_ACTUAL_G ?? 0) +
                (obj.TXT_ACTUAL_H ?? 0) +
                (obj.TXT_ACTUAL_I ?? 0);

            obj.DISPLAY_RPT_I =
                (obj.TXT_RPT_G ?? 0) +
                (obj.TXT_RPT_H ?? 0) +
                (obj.TXT_RPT_I ?? 0);

            obj.DISPLAY_BAL_I =
                (obj.TXT_BAL_G ?? 0) +
                (obj.TXT_BAL_H ?? 0) +
                (obj.TXT_BAL_I ?? 0);
        }

        return Json(obj,
            JsonRequestBehavior.AllowGet);
    }
}


@model YourProject.Models.BFProductionModel

<div class="container mt-3">

    <div class="row mb-3">

        <div class="col-md-3">
            <input type="date"
                   id="txtDate"
                   class="form-control">
        </div>

        <div class="col-md-2">
            <button class="btn btn-primary"
                    onclick="LoadData()">

                Load Data

            </button>
        </div>

    </div>


    <table class="table table-bordered text-center">

        <thead class="table-dark">

            <tr>
                <th>Furnace</th>
                <th>Actual</th>
                <th>Reported</th>
                <th>Balance</th>
            </tr>

        </thead>

        <tbody>

            <tr>
                <td>G</td>

                <td>
                    <input type="text"
                           id="TXT_ACTUAL_G"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_RPT_G"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_BAL_G"
                           class="form-control">
                </td>
            </tr>

            <tr>
                <td>H</td>

                <td>
                    <input type="text"
                           id="TXT_ACTUAL_H"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_RPT_H"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_BAL_H"
                           class="form-control">
                </td>
            </tr>

            <tr>
                <td>I</td>

                <td>
                    <input type="text"
                           id="TXT_ACTUAL_I"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_RPT_I"
                           class="form-control">
                </td>

                <td>
                    <input type="text"
                           id="TXT_BAL_I"
                           class="form-control">
                </td>
            </tr>

        </tbody>

    </table>

</div>


<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<script>

    function LoadData() {

        $.ajax({

            url: '/Home/GetBFProductionTracking',

            type: 'GET',

            data: {
                ctl_date_time_prod:
                    $("#txtDate").val()
            },

            success: function (res) {

                $("#TXT_ACTUAL_G").val(res.TXT_ACTUAL_G);
                $("#TXT_RPT_G").val(res.TXT_RPT_G);
                $("#TXT_BAL_G").val(res.TXT_BAL_G);

                $("#TXT_ACTUAL_H").val(res.TXT_ACTUAL_H);
                $("#TXT_RPT_H").val(res.TXT_RPT_H);
                $("#TXT_BAL_H").val(res.TXT_BAL_H);

                $("#TXT_ACTUAL_I").val(res.TXT_ACTUAL_I);
                $("#TXT_RPT_I").val(res.TXT_RPT_I);
                $("#TXT_BAL_I").val(res.TXT_BAL_I);

            }

        });

    }

</script>

