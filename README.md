@{
    ViewBag.Title = ProcessTrends.App.PageTitle;
}
@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" />
    <style>
        body {
            background: white;
            padding: 20px;
        }

        .card {
            margin-top:20px;
            margin-left:400px;
            width:600px;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #loader {
            display: none;
            text-align: center;
            font-weight: bold;
            color: #0d6efd;
            margin-bottom: 10px;
        }

        .table th {
            /*background-color: #0d47a1;*/
            color: white;
        }
    </style>
}
<div class="app-content">
    @Html.Partial("_Header")
    <div class="main-content">
        <div class="container" style="background-color:white;">
            <div class="card">
                <h3 class="text-center mb-3" style="font-family:Courier New, Courier, monospace; font-weight:bold;" >Pile Mat Wise Quality Data</h3>
                <div id="loader">Loading data...</div>
                <table class="table table-bordered table-striped table-hover text-center" id="finesTable">
                    <thead>
                        <tr>
                            <th>Element</th>
                            <th>Return Fines</th>
                            <th>Wet Fines</th>
                            <th>Dry Fines</th>
                            <th>Dry Fines 500TPH</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td colspan="5">Loading...</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="trendModal" tabindex="-1">
            <div class="modal-dialog modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title">30 Days Trend</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                    </div>
                    <div class="modal-body">
                        <div id="trendChart" style="height:400px;"></div>
                    </div>
                </div>
            </div>
        </div>


    </div>
</div>
@section scripts {    
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.5.0/dist/echarts.min.js"></script>

    <script>
        let chartInstance = null;
        $(document).ready(function () {
            loadFinesData();
        });
        $(document).on("click", ".chart-cell", function () {
            let type = $(this).data("type");
            let value = $(this).text().trim();
            loadTrend(type, value);
        });

        function loadFinesData() {
            $('#loader').show();
            $.ajax({
                url: '/Ore_Beneficiation/GetFinesData',
                type: 'GET',
                dataType: 'json',
                success: function (res) {                                        
                    if (res && res.error) {
                        showError(res.error);
                    }                    
                    else if (res && res.data) {
                        renderTable(res.data);
                    }
                    else {
                        renderTable(res);
                    }

                    $('#loader').hide();
                },

                error: function () {
                    $('#loader').hide();
                    showError("Error loading data");
                }
            });
        }

     
        function showError(msg) {
            $('#finesTable tbody').html(
                `<tr><td colspan="5" class="text-danger">${msg}</td></tr>`
            );
        }

      
        function getValue(val) {
            if (val === null || val === undefined || val === "" || val === "null") {
                return '-';
            }
            return val;
        }

       
        function renderTable(data) {

            let html = '';

            if (!data || data.length === 0) {
                html = "<tr><td colspan='5'>No Data Found</td></tr>";
            }
            else {
                data.forEach(item => {

                    html += `
            <tr>
                <td class="chart-cell" data-type="ELEMENT">${item.ELEMENT}</td>
                <td class="chart-cell" data-type="RETURN_FINES">${item.RETURN_FINES}</td>
                <td class="chart-cell" data-type="WET_FINES">${item.WET_FINES}</td>
                <td class="chart-cell" data-type="DRY_FINES">${item.DRY_FINES}</td>
                <td class="chart-cell" data-type="DRY_FINES_500TPH">${item.DRY_FINES_500TPH}</td>
            </tr>`;
                });
            }

            $("#finesTable tbody").html(html);
        }
        function loadTrend(type, value) {
            $.ajax({
                url: '/Ore_Beneficiation/GetFinesTrend',
                type: 'GET',
                data: {
                    type: type,
                    value: value
                },
                success: function (res) {

                    $("#trendModal").modal("show");

                    drawChart(res);
                },
                error: function () {
                    alert("Chart load failed");
                }
            });
        }
        function drawChart(data) {

            echarts.init(document.getElementById("trendChart"))
                .setOption({
                    xAxis: {
                        type: 'category',
                        data: data.map(d => d.DATE)
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [{
                        type: 'line',
                        data: data.map(d => d.VALUE)
                    }]
                });
        }


    </script>
  
}

  public JsonResult GetFinesTrend(string type, string value)
        {
            List<object> list = new List<object>();           
            using (OracleConnection con = new OracleConnection(mycon))
            {
                con.Open();
                string column = "";                
                switch (type.ToUpper())
                {
                    case "AL2O3":
                        column = "RETURN_FINES_AL2O3";
                        break;

                    case "SIO2":
                        column = "RETURN_FINES_SIO2";
                        break;

                    case "P":
                        column = "RETURN_FINES_P";
                        break;

                    case "K2O":
                        column = "RETURN_FINES_K2O";
                        break;

                    default:
                        column = "RETURN_FINES_AL2O3";
                        break;
                }

                string query = $@"
            SELECT 
                TRUNC(TIMESTAMP) AS TREND_DATE,
                {column} AS VALUE
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE TRUNC(TIMESTAMP) >= TRUNC(SYSDATE - 30)
            ORDER BY TIMESTAMP";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        while (dr.Read())
                        {
                            list.Add(new
                            {
                                DATE = Convert.ToDateTime(dr["TREND_DATE"]).ToString("yyyy-MM-dd"),
                                VALUE = dr["VALUE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["VALUE"])
                            });
                        }
                    }
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
