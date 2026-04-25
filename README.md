@{
    ViewBag.Title = "PileMatWiseQualityData";
}
<!DOCTYPE html>
<html>
<head>
    <title>PileMatWiseQualityData</title>    
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
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="card">
            <h3 class="text-center mb-3">Pile Mat Wise Quality Data</h3>           
            <div id="loader">Loading data...</div>
            <table class="table table-bordered text-center" id="finesTable">
                <thead class="table-dark">
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
            <div id="rowCount" class="mt-2 fw-bold"></div>
        </div>
    </div>    
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>

$(document).ready(function () {
    loadFinesData();
});

function loadFinesData() {   
    $.ajax({
        url: '/Home/GetFinesData',
        type: 'GET',
        dataType: 'json',
        success: function (res) {
            renderTable(res);
            showRowCount(res);            
        },
        error: function (err) {         
            console.log("Error:", err);
            $('#finesTable tbody').html(
                "<tr><td colspan='5' style='color:red;'>Error loading data</td></tr>"
            );
        }
    });
}
function renderTable(data) {
    var html = '';
    $.each(data, function (i, item) {
        html += '<tr>';
        html += '<td>' + (item.ELEMENT || '-') + '</td>';
        html += '<td>' + (item.RETURN_FINES || '-') + '</td>';
        html += '<td>' + (item.WET_FINES || '-') + '</td>';
        html += '<td>' + (item.DRY_FINES || '-') + '</td>';
        html += '<td>' + (item.DRY_FINES_500TPH || '-') + '</td>';
        html += '</tr>';
    });

    $('#finesTable tbody').html(html);
}

function showRowCount(data) {
    var count = data.length;
    $('#rowCount').text("Total Rows: " + count);
}
    </script>
</body>
</html>
