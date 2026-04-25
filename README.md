@{
    ViewBag.Title = "PileMatWiseQualityData";
}
<!DOCTYPE html>
<html>
<head>
    <title>PileMatWiseQualityData</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

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
</head>

<body>
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

            <div id="rowCount" class="mt-2 fw-bold text-end"></div>

        </div>
    </div>

    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

    <script>
        $(document).ready(function () {
            loadFinesData();

            // Optional Auto Refresh (every 30 sec)
            // setInterval(loadFinesData, 30000);
        });

        function loadFinesData() {

            $('#loader').show();   // Show loader

            $.ajax({
                url: '/Home/GetFinesData',
                type: 'GET',
                dataType: 'json',

                success: function (res) {

                    // Handle error from controller
                    if (res && res.error) {
                        $('#finesTable tbody').html(
                            "<tr><td colspan='5' class='text-danger'>" + res.error + "</td></tr>"
                        );
                        $('#rowCount').text("");
                    }
                    else {
                        renderTable(res);
                        showRowCount(res);
                    }

                    $('#loader').hide();
                },

                error: function () {
                    $('#loader').hide();
                    $('#finesTable tbody').html(
                        "<tr><td colspan='5' class='text-danger'>Error loading data</td></tr>"
                    );
                    $('#rowCount').text("");
                }
            });
        }

        function renderTable(data) {

            var html = '';

            if (!data || data.length === 0) {
                html = "<tr><td colspan='5'>No data found</td></tr>";
            }
            else {
                $.each(data, function (i, item) {

                    html += '<tr>';

                    html += '<td>' + (item.ELEMENT ?? '-') + '</td>';
                    html += '<td>' + (item.RETURN_FINES ?? '-') + '</td>';
                    html += '<td>' + (item.WET_FINES ?? '-') + '</td>';
                    html += '<td>' + (item.DRY_FINES ?? '-') + '</td>';
                    html += '<td>' + (item.DRY_FINES_500TPH ?? '-') + '</td>';

                    html += '</tr>';
                });
            }

            $('#finesTable tbody').html(html);
        }

        function showRowCount(data) {
            var count = (data && data.length) ? data.length : 0;
            $('#rowCount').text("Total Rows: " + count);
        }

    </script>

</body>
</html>
