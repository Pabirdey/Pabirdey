@{
    ViewBag.Title = "TLC Master";
}

<div class="container-fluid">

    <div class="row">

        <div class="col-md-8">

            <h4>TLC MASTER</h4>

            <div id="message"></div>

            <div class="table-responsive">

                <table id="tblTLC"
                       class="table table-bordered table-sm">

                    <thead>
                        <tr>
                            <th>SL NO</th>
                            <th>TLC NO</th>
                            <th>MATURITY LIFE</th>
                            <th>TLC SIZE</th>
                        </tr>
                    </thead>

                    <tbody id="tblTLCBody">

                    </tbody>

                </table>

            </div>

        </div>

    </div>

</div>


<script>

    $(document).ready(function () {

        GetTLCMaster();

    });


    function GetTLCMaster() {

        $.ajax({

            url: '@Url.Action("GetTLCMaster", "TLC")',

            type: 'GET',

            dataType: 'json',

            success: function (response) {

                if (response.success) {

                    BindTLCMaster(response.data);

                }
                else {

                    $("#message").html(
                        '<div class="alert alert-danger">' +
                        response.message +
                        '</div>'
                    );

                }

            },

            error: function (xhr, status, error) {

                $("#message").html(
                    '<div class="alert alert-danger">' +
                    'Server Error : ' + error +
                    '</div>'
                );

            }

        });

    }


    function BindTLCMaster(data) {

        var tbody = $("#tblTLCBody");

        tbody.empty();


        if (data == null || data.length == 0) {

            tbody.append(
                '<tr>' +
                '<td colspan="4" class="text-center">' +
                'No data found' +
                '</td>' +
                '</tr>'
            );

            return;
        }


        $.each(data, function (index, item) {

            var row = "";

            row += "<tr>";

            // Serial number
            row += "<td>" +
                   (index + 1) +
                   "</td>";

            // TLC NO
            row += "<td>" +
                   item.TLC_NO +
                   "</td>";

            // MATURITY LIFE
            row += "<td>" +
                   item.MATURITY_LIFE +
                   "</td>";

            // TLC SIZE
            row += "<td>" +
                   item.TLC_SIZE +
                   "</td>";

            row += "</tr>";

            tbody.append(row);

        });

    }

</script>


using System;
using System.Collections.Generic;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class TLCController : Controller
{
    // Page load
    [HttpGet]
    public ActionResult Index()
    {
        return View();
    }


    // AJAX call
    [HttpGet]
    public JsonResult GetTLCMaster()
    {
        List<TlcMasterModel> list = new List<TlcMasterModel>();

        try
        {
            using (OracleConnection con =
                new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                string query = @"
                    SELECT TLC_NO,
                           MATURITY_LIFE,
                           TLC_SIZE
                    FROM T_TLC_MASTER
                    ORDER BY TLC_NO";

                using (OracleCommand cmd =
                    new OracleCommand(query, con))
                {
                    using (OracleDataReader dr =
                        cmd.ExecuteReader())
                    {
                        while (dr.Read())
                        {
                            TlcMasterModel model =
                                new TlcMasterModel();

                            if (dr["TLC_NO"] != DBNull.Value)
                            {
                                model.TLC_NO =
                                    Convert.ToInt32(dr["TLC_NO"]);
                            }

                            if (dr["MATURITY_LIFE"] != DBNull.Value)
                            {
                                model.MATURITY_LIFE =
                                    Convert.ToInt32(
                                        dr["MATURITY_LIFE"]);
                            }

                            if (dr["TLC_SIZE"] != DBNull.Value)
                            {
                                model.TLC_SIZE =
                                    dr["TLC_SIZE"].ToString();
                            }

                            list.Add(model);
                        }
                    }
                }
            }

            return Json(new
            {
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
}
