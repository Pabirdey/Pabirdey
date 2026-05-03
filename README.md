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
        <div class="container">
            <div class="card">
                <h3 class="text-center">Pile Mat Wise Quality Data</h3>
                <div id="loader">Loading...</div>
                <table class="table table-bordered text-center" id="finesTable">
                    <thead>
                        <tr>
                            <th>Element</th>
                            <th>Return Fines</th>
                            <th>Wet Fines</th>
                            <th>Dry Fines</th>
                            <th>Dry Fines 500TPH</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>
</div>

<div class="modal fade" id="trendModal" tabindex="-1" role="dialog">
    <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">30 Days Trend</h5>
                <button type="button" class="close" data-dismiss="modal">
                    <span>&times;</span>
                </button>
            </div>
            <div class="modal-body">
                <div id="trendChart" style="height:400px;"></div>
            </div>
        </div>
    </div>
</div>

@section scripts {    
    @*<script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>*@
    <!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
<!-- jQuery (optional for your existing code) -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<!-- Bootstrap JS Bundle -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.5.0/dist/echarts.min.js"></script>

    <script>
        let chartInstance = null;
        $(document).ready(function () {
            loadFinesData();
        });
        $(document).on("click", ".chart-cell", function () {
            let type = $(this).data("type");
            loadTrend(type);
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
                <td>${item.ELEMENT}</td>

                <td class="chart-cell" data-type="RETURN_FINES">${item.RETURN_FINES}</td>

                <td class="chart-cell" data-type="WET_FINES">${item.WET_FINES}</td>

                <td class="chart-cell" data-type="DRY_FINES">${item.DRY_FINES}</td>

                <td class="chart-cell" data-type="DRY_FINES_500TPH">${item.DRY_FINES_500TPH}</td>
            </tr>`;
                });
            }

            $("#finesTable tbody").html(html);
        }

       function loadTrend(type) {

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesTrend',
        type: 'GET',
        data: { type: type },
        success: function (res) {

            // ✅ Bootstrap 5 safe modal open
            var modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();

            drawChart(res);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}

        function drawChart(data) {

            if (chartInstance != null) {
                chartInstance.dispose();
            }

            chartInstance = echarts.init(document.getElementById("trendChart"));

            chartInstance.setOption({
                tooltip: { trigger: 'axis' },

                xAxis: {
                    type: 'category',
                    data: data.map(x => x.DATE)
                },

                yAxis: {
                    type: 'value'
                },

                series: [{
                    type: 'line',
                    smooth: true,
                    data: data.map(x => x.VALUE),
                    lineStyle: { width: 3 }
                }]
            });
        }


    </script>
  
}

