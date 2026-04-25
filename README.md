
@{
    ViewBag.Title = "PileMatWiseQualityData";
}


<html>
<head>
    <title>PileMatWiseQualityData</title>
    <h2>PileMatWiseQualityData</h2>
    <body>
        <table class="table table-bordered" id="finesTable">
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
        <div id="rowCount" style="margin-top:10px;font-weight:bold;"></div>
        <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
        <script>

$(document).ready(function () {
    loadFinesData();   // call function on page load
});


// ✅ MAIN FUNCTION
function loadFinesData() {

    $.ajax({
        url: '/Home/GetFinesData',
        type: 'GET',
        dataType: 'json',

        success: function (res) {

            renderTable(res);   // separate rendering function
            showRowCount(res);  // show total rows
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
        html += '<td>' + item.ELEMENT + '</td>';
        html += '<td>' + item.RETURN_FINES + '</td>';
        html += '<td>' + item.WET_FINES + '</td>';
        html += '<td>' + item.DRY_FINES + '</td>';
        html += '<td>' + item.DRY_FINES_500TPH + '</td>';
        html += '</tr>';
    });

    $('#finesTable tbody').html(html);
}
function showRowCount(data) {

    var count = data.length;   // total rows

    $('#rowCount').text("Total Rows: " + count);
}
setInterval(function () {
    loadFinesData();
}, 30000);

        </script>

    </body>
</head>
</html>
