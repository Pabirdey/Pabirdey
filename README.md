@{
    ViewBag.Title = "BF Production";
}

<!DOCTYPE html>

<html>

<head>

    <meta name="viewport"
          content="width=device-width" />

    <title>
        BF Production
    </title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
          rel="stylesheet" />

</head>

<body>

    <div class="container mt-4">

        <div class="card shadow">

            <div class="card-header bg-primary text-white">

                <h4>
                    G & H Furnace Production
                </h4>

            </div>

            <div class="card-body">

                <!-- DATE -->

                <div class="row mb-3">

                    <div class="col-md-3">

                        <label>
                            Production Date
                        </label>

                        <input type="date"
                               id="txtDate"
                               class="form-control" />

                    </div>

                    <div class="col-md-2 mt-4">

                        <button class="btn btn-success w-100"
                                onclick="LoadData()">

                            Load Data

                        </button>

                    </div>

                </div>

                <!-- TABLE -->

                <div class="table-responsive">

                    <table class="table table-bordered text-center align-middle">

                        <thead class="table-dark">

                            <tr>

                                <th>
                                    Furnace
                                </th>

                                <th>
                                    Actual
                                </th>

                                <th>
                                    Reported
                                </th>

                                <th>
                                    Balance
                                </th>

                                <th>
                                    Actual TD
                                </th>

                                <th>
                                    Reported TD
                                </th>

                                <th>
                                    LD1
                                </th>

                                <th>
                                    LD2
                                </th>

                                <th>
                                    LD3
                                </th>

                                <th>
                                    MRD
                                </th>

                                <th>
                                    TP
                                </th>

                            </tr>

                        </thead>

                        <tbody>

                            <!-- G FURNACE -->

                            <tr>

                                <td>
                                    G
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtActualG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtReportedG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtBalanceG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtActualTDG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtReportedTDG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD1G"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD2G"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD3G"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtMRDG"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtTPG"
                                           class="form-control text-center">
                                </td>

                            </tr>

                            <!-- H FURNACE -->

                            <tr>

                                <td>
                                    H
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtActualH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtReportedH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtBalanceH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtActualTDH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtReportedTDH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD1H"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD2H"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtLD3H"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtMRDH"
                                           class="form-control text-center">
                                </td>

                                <td>
                                    <input type="text"
                                           id="txtTPH"
                                           class="form-control text-center">
                                </td>

                            </tr>

                        </tbody>

                    </table>

                </div>

            </div>

        </div>

    </div>

    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <script>

        //--------------------------------------
        // LOAD DATA
        //--------------------------------------

        function LoadData() {

            var prodDate =
                $("#txtDate").val();

            if (prodDate == "") {

                alert("Select Date");

                return;
            }

            $.ajax({

                url: '/BF/LoadData',

                type: 'GET',

                data: {
                    prodDate: prodDate
                },

                success: function (res) {

                    console.log(res);

                    $.each(res.Furnaces,
                    function (i, row) {

                        //----------------------------------
                        // G FURNACE
                        //----------------------------------

                        if (row.FURNACE == "G") {

                            $("#txtActualG")
                                .val(row.ACTUAL);

                            $("#txtReportedG")
                                .val(row.REPORTED);

                            $("#txtBalanceG")
                                .val(row.BALANCE);

                            $("#txtActualTDG")
                                .val(row.ACTUAL_TD);

                            $("#txtReportedTDG")
                                .val(row.REPORTED_TD);

                            $("#txtLD1G")
                                .val(row.LD1_TONS);

                            $("#txtLD2G")
                                .val(row.LD2_TONS);

                            $("#txtLD3G")
                                .val(row.LD3_TONS);

                            $("#txtMRDG")
                                .val(row.MRDTP_TONS);

                            $("#txtTPG")
                                .val(row.NOOFTP);
                        }

                        //----------------------------------
                        // H FURNACE
                        //----------------------------------

                        if (row.FURNACE == "H") {

                            $("#txtActualH")
                                .val(row.ACTUAL);

                            $("#txtReportedH")
                                .val(row.REPORTED);

                            $("#txtBalanceH")
                                .val(row.BALANCE);

                            $("#txtActualTDH")
                                .val(row.ACTUAL_TD);

                            $("#txtReportedTDH")
                                .val(row.REPORTED_TD);

                            $("#txtLD1H")
                                .val(row.LD1_TONS);

                            $("#txtLD2H")
                                .val(row.LD2_TONS);

                            $("#txtLD3H")
                                .val(row.LD3_TONS);

                            $("#txtMRDH")
                                .val(row.MRDTP_TONS);

                            $("#txtTPH")
                                .val(row.NOOFTP);
                        }

                    });

                },

                error: function (err) {

                    console.log(err);

                    alert("Error Loading Data");

                }

            });

        }

    </script>

</body>

</html>

// STEP 4
// CONTROLLER
// FILE: Controllers/BFController.cs

using Oracle.ManagedDataAccess.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Web.Mvc;
using YourProject.Models;

namespace YourProject.Controllers
{
    public class BFController : Controller
    {
        string conStr =
            ConfigurationManager
            .ConnectionStrings["OracleCon"]
            .ConnectionString;

        //------------------------------------------------
        // PAGE LOAD
        //------------------------------------------------

        public ActionResult Index()
        {
            return View();
        }

        //------------------------------------------------
        // AJAX LOAD
        //------------------------------------------------

        public JsonResult LoadData(string prodDate)
        {
            BFViewModel model =
                new BFViewModel();

            model.Furnaces =
                new List<FurnaceModel>();

            DateTime dt =
                Convert.ToDateTime(prodDate);

            string[] furnaces =
                { "G", "H" };

            using (OracleConnection con =
                   new OracleConnection(conStr))
            {
                con.Open();

                foreach (string furnace
                         in furnaces)
                {
                    FurnaceModel row =
                        new FurnaceModel();

                    row.FURNACE =
                        furnace;

                    //----------------------------------------
                    // CHECK TRACKING RECORD
                    //----------------------------------------

                    string chkQry = @"

                    SELECT COUNT(*)

                    FROM DEMO.T_BF_PRODUCTION_TRACKING

                    WHERE TIMESTAMP=:PDATE

                    AND FURNACE=:FURNACE";

                    OracleCommand chkCmd =
                        new OracleCommand(
                            chkQry, con);

                    chkCmd.Parameters.Add(
                        "PDATE",
                        OracleDbType.Date)
                        .Value = dt;

                    chkCmd.Parameters.Add(
                        "FURNACE",
                        OracleDbType.Varchar2)
                        .Value = furnace;

                    int count =
                        Convert.ToInt32(
                        chkCmd.ExecuteScalar());

                    //----------------------------------------
                    // IF RECORD EXISTS
                    //----------------------------------------

                    if (count > 0)
                    {
                        string qry = @"

                        SELECT

                        NVL(ACTUAL,0),

                        NVL(REPORTED,0),

                        NVL(BALANCE,0)

                        FROM DEMO.T_BF_PRODUCTION_TRACKING

                        WHERE TIMESTAMP=:PDATE

                        AND FURNACE=:FURNACE";

                        OracleCommand cmd =
                            new OracleCommand(
                                qry, con);

                        cmd.Parameters.Add(
                            "PDATE",
                            OracleDbType.Date)
                            .Value = dt;

                        cmd.Parameters.Add(
                            "FURNACE",
                            OracleDbType.Varchar2)
                            .Value = furnace;

                        OracleDataReader dr =
                            cmd.ExecuteReader();

                        if (dr.Read())
                        {
                            row.ACTUAL =
                                Convert.ToDecimal(
                                    dr[0]);

                            row.REPORTED =
                                Convert.ToDecimal(
                                    dr[1]);

                            row.BALANCE =
                                Convert.ToDecimal(
                                    dr[2]);
                        }
                    }

                    //----------------------------------------
                    // ELSE CALCULATE
                    //----------------------------------------

                    else
                    {
                        string actualQry = @"

                        SELECT
                        NVL(SUM(NET_WT),0)

                        FROM DEMO.T_LADLE_DETAILS

                        WHERE LADLE_FLEND_TIME
                        >= :FROMDATE

                        AND LADLE_FLEND_TIME
                        < :TODATE

                        AND DESTINATION<>'R'

                        AND FUR_NAME=:FURNACE";

                        OracleCommand actualCmd =
                            new OracleCommand(
                                actualQry, con);

                        actualCmd.Parameters.Add(
                            "FROMDATE",
                            OracleDbType.Date)
                            .Value =
                            dt.AddHours(6);

                        actualCmd.Parameters.Add(
                            "TODATE",
                            OracleDbType.Date)
                            .Value =
                            dt.AddDays(1)
                            .AddHours(6);

                        actualCmd.Parameters.Add(
                            "FURNACE",
                            OracleDbType.Varchar2)
                            .Value = furnace;

                        row.ACTUAL =
                            Convert.ToDecimal(
                            actualCmd.ExecuteScalar());

                        //------------------------------------
                        // BALANCE
                        //------------------------------------

                        string balQry = @"

                        SELECT

                        NVL(
                        SUM(
                        NVL(ACTUAL,0)
                        -
                        NVL(REPORTED,0)
                        ),0)

                        FROM DEMO.T_BF_PRODUCTION_TRACKING

                        WHERE TIMESTAMP >=
                        TRUNC(:PDATE,'MON')

                        AND TIMESTAMP < :PDATE

                        AND FURNACE=:FURNACE";

                        OracleCommand balCmd =
                            new OracleCommand(
                                balQry, con);

                        balCmd.Parameters.Add(
                            "PDATE",
                            OracleDbType.Date)
                            .Value = dt;

                        balCmd.Parameters.Add(
                            "FURNACE",
                            OracleDbType.Varchar2)
                            .Value = furnace;

                        row.BALANCE =
                            Convert.ToDecimal(
                            balCmd.ExecuteScalar());

                        //------------------------------------
                        // REPORTED
                        //------------------------------------

                        row.REPORTED =
                            row.ACTUAL
                            +
                            row.BALANCE;

                        //------------------------------------
                        // FINAL BALANCE
                        //------------------------------------

                        row.BALANCE =
                            row.ACTUAL
                            -
                            row.REPORTED
                            +
                            row.BALANCE;
                    }

                    //----------------------------------------
                    // TD TOTAL
                    //----------------------------------------

                    string tdQry = @"

                    SELECT

                    NVL(SUM(ACTUAL),0),

                    NVL(SUM(REPORTED),0)

                    FROM DEMO.T_BF_PRODUCTION_TRACKING

                    WHERE TIMESTAMP >=
                    TRUNC(:PDATE,'MON')

                    AND TIMESTAMP <= :PDATE

                    AND FURNACE=:FURNACE";

                    OracleCommand tdCmd =
                        new OracleCommand(
                            tdQry, con);

                    tdCmd.Parameters.Add(
                        "PDATE",
                        OracleDbType.Date)
                        .Value = dt;

                    tdCmd.Parameters.Add(
                        "FURNACE",
                        OracleDbType.Varchar2)
                        .Value = furnace;

                    OracleDataReader tdDr =
                        tdCmd.ExecuteReader();

                    if (tdDr.Read())
                    {
                        row.ACTUAL_TD =
                            Convert.ToDecimal(
                            tdDr[0]);

                        row.REPORTED_TD =
                            Convert.ToDecimal(
                            tdDr[1]);
                    }

                    //----------------------------------------
                    // LD1
                    //----------------------------------------

                    row.LD1_TONS =
                        GetDestinationTotal(
                        con, dt,
                        furnace,
                        "LD1");

                    //----------------------------------------
                    // LD2
                    //----------------------------------------

                    row.LD2_TONS =
                        GetDestinationTotal(
                        con, dt,
                        furnace,
                        "LD2");

                    //----------------------------------------
                    // LD3
                    //----------------------------------------

                    row.LD3_TONS =
                        GetDestinationTotal(
                        con, dt,
                        furnace,
                        "LD3");

                    //----------------------------------------
                    // MRD
                    //----------------------------------------

                    row.MRDTP_TONS =
                        GetDestinationTotal(
                        con, dt,
                        furnace,
                        "MRD");

                    //----------------------------------------
                    // TP
                    //----------------------------------------

                    row.NOOFTP =
                        GetTP(
                        con, dt,
                        furnace);

                    //----------------------------------------
                    // DISPLAY TOTALS
                    //----------------------------------------

                    model.DISPLAY_ACTUAL +=
                        row.ACTUAL;

                    model.DISPLAY_REPORTED +=
                        row.REPORTED;

                    model.DISPLAY_BALANCE +=
                        row.BALANCE;

                    model.DISPLAY_ACTUAL_TD +=
                        row.ACTUAL_TD;

                    model.DISPLAY_REPORTED_TD +=
                        row.REPORTED_TD;

                    model.Furnaces.Add(row);
                }
            }

            return Json(
                model,
                JsonRequestBehavior.AllowGet);
        }

        //------------------------------------------------
        // COMMON METHOD
        //------------------------------------------------

        public decimal GetDestinationTotal(
            OracleConnection con,
            DateTime dt,
            string furnace,
            string destination)
        {
            string qry = @"

            SELECT
            NVL(SUM(NET_WT),0)

            FROM DEMO.T_LADLE_DETAILS

            WHERE LADLE_FLEND_TIME
            >= :FROMDATE

            AND LADLE_FLEND_TIME
            < :TODATE

            AND DESTINATION=:DEST

            AND FUR_NAME=:FURNACE";

            OracleCommand cmd =
                new OracleCommand(
                    qry, con);

            cmd.Parameters.Add(
                "FROMDATE",
                OracleDbType.Date)
                .Value =
                dt.AddHours(6);

            cmd.Parameters.Add(
                "TODATE",
                OracleDbType.Date)
                .Value =
                dt.AddDays(1)
                .AddHours(6);

            cmd.Parameters.Add(
                "DEST",
                OracleDbType.Varchar2)
                .Value =
                destination;

            cmd.Parameters.Add(
                "FURNACE",
                OracleDbType.Varchar2)
                .Value =
                furnace;

            return Convert.ToDecimal(
                cmd.ExecuteScalar());
        }

        //------------------------------------------------
        // TP
        //------------------------------------------------

        public decimal GetTP(
            OracleConnection con,
            DateTime dt,
            string furnace)
        {
            string qry = @"

            SELECT
            NVL(SUM(FILL_STATUS),0)

            FROM DEMO.T_LADLE_DETAILS

            WHERE LADLE_FLEND_TIME
            >= :FROMDATE

            AND LADLE_FLEND_TIME
            < :TODATE

            AND TRP_NO<=50

            AND RET_FLAG='N'

            AND FUR_NAME=:FURNACE";

            OracleCommand cmd =
                new OracleCommand(
                    qry, con);

            cmd.Parameters.Add(
                "FROMDATE",
                OracleDbType.Date)
                .Value =
                dt.AddHours(6);

            cmd.Parameters.Add(
                "TODATE",
                OracleDbType.Date)
                .Value =
                dt.AddDays(1)
                .AddHours(6);

            cmd.Parameters.Add(
                "FURNACE",
                OracleDbType.Varchar2)
                .Value =
                furnace;

            return Convert.ToDecimal(
                cmd.ExecuteScalar());
        }
    }
}
// STEP 3
// MODEL
// FILE: Models/BFModel.cs

using System.Collections.Generic;

namespace YourProject.Models
{
    public class FurnaceModel
    {
        public string FURNACE { get; set; }

        public decimal ACTUAL { get; set; }

        public decimal REPORTED { get; set; }

        public decimal BALANCE { get; set; }

        public decimal ACTUAL_TD { get; set; }

        public decimal REPORTED_TD { get; set; }

        public decimal LD1_TONS { get; set; }

        public decimal LD2_TONS { get; set; }

        public decimal LD3_TONS { get; set; }

        public decimal MRDTP_TONS { get; set; }

        public decimal NOOFTP { get; set; }
    }

    public class BFViewModel
    {
        public List<FurnaceModel> Furnaces { get; set; }

        public decimal DISPLAY_ACTUAL { get; set; }

        public decimal DISPLAY_REPORTED { get; set; }

        public decimal DISPLAY_BALANCE { get; set; }

        public decimal DISPLAY_ACTUAL_TD { get; set; }

        public decimal DISPLAY_REPORTED_TD { get; set; }
    }
}