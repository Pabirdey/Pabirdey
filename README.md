@{
    ViewBag.Title = ProcessTrends.App.PageTitle;
}
@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" media="screen">

<style>
    body {
        background: #f4f6f9;
        padding: 20px;
    }

    .card {
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
        background-color: #0d47a1;
        color: white;
    }
</style>
}
<div class="app-content">
    <!-- start: TOP NAVBAR -->
    @Html.Partial("_Header")
    <!-- end: TOP NAVBAR -->
    <div class="main-content">
        <div class="container">
            <div class="card">
                <h3 class="text-center mb-3">Pile Mat Wise Quality Data</h3>
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
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>   
</div>

@section scripts {
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script src="@Url.Content("~/bower_components/echarts/echarts.min.js")"></script>
    <script src="@Url.Content("~/bower_components/Math.js/Math.min.js")"></script>
    <!-- start: Packet JAVASCRIPTS -->
    <script src="@Url.Content("~/Content/js/echart-custom-options/common.js")"></script>
    <script src="@Url.Content("~/Content/js/echart-custom-options/oven-health-visualisation.js")"></script>
    <script type="text/javascript">
        $(document).ready(function () {
            loadFinesData();
        });

        function loadFinesData() {

            $('#loader').show();

            $.ajax({
                url: '/Ore_Beneficiation/GetFinesData',
                type: 'GET',
                dataType: 'json',

                success: function (res) {

                    if (res && res.error) {
                        $('#finesTable tbody').html(
                            "<tr><td colspan='5' class='text-danger'>" + res.error + "</td></tr>"
                        );
                    }
                    else {
                        renderTable(res);
                    }

                    $('#loader').hide();
                },

                error: function () {
                    $('#loader').hide();
                    $('#finesTable tbody').html(
                        "<tr><td colspan='5' class='text-danger'>Error loading data</td></tr>"
                    );
                }
            });
        }

        // Handle NULL / empty values
        function getValue(val) {
            if (val === null || val === undefined || val === "" || val === "null") {
                return '-';
            }
            return val;
        }

        function renderTable(data) {

            var html = '';

            if (!data || data.length === 0) {
                html = "<tr><td colspan='5'>No data found</td></tr>";
            }
            else {
                $.each(data, function (i, item) {

                    html += '<tr>';
                    html += '<td>' + getValue(item.ELEMENT) + '</td>';
                    html += '<td>' + getValue(item.RETURN_FINES) + '</td>';
                    html += '<td>' + getValue(item.WET_FINES) + '</td>';
                    html += '<td>' + getValue(item.DRY_FINES) + '</td>';
                    html += '<td>' + getValue(item.DRY_FINES_500TPH) + '</td>';
                    html += '</tr>';

                });
            }

            $('#finesTable tbody').html(html);
        }
        </script>
