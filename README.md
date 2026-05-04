
@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>PileQuality</title>
    <link href="~/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/bootstrap-datepicker.min.css" rel="stylesheet" />
    <style>
        body {
            background: white;
            padding: 20px;
        }

        .card {
            margin-top: 20px;
            margin-left: 300px;
            width: 750px;
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

        .chart-cell {
            cursor: pointer;
            color: #0d6efd;
        }

            .chart-cell:hover {
                background: #f2f2f2;
            }
    </style>
</head>
<body>
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
    
    <!-- MODAL -->
    <div class="modal fade" id="trendModal" tabindex="-1">
        <div class="modal-dialog modal-lg modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title"></h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div id="trendChart" style="height:400px;"></div>
                </div>
            </div>
        </div>
        </div>
    <script src="~/js/Jquey3.6.0.min.js"></script>
    <script src="~/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/bootstrap-datepicker.min.js"></script>    
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.5.0/dist/echarts.min.js"></script>
    <script>

let chartInstance = null;

$(document).ready(function () {
    loadFinesData();
});


$(document).on("click", ".chart-cell", function () {
    let type = $(this).data("type");
    let element = $(this).data("element");
    loadTrend(type, element);
});


function loadFinesData() {
    $('#loader').show();
    $.ajax({
        url: '/RmbbPile/GetFinesData',
        type: 'GET',
        success: function (res) {
            $('#loader').hide();
            renderTable(res.data || res);
        },
        error: function () {
            $('#loader').hide();
            alert("Error loading data");
        }
    });
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

                <td class="chart-cell" data-type="RETURN_FINES" data-element="${item.ELEMENT}">
                    ${item.RETURN_FINES}
                </td>

                <td class="chart-cell" data-type="WET_FINES" data-element="${item.ELEMENT}">
                    ${item.WET_FINES}
                </td>

                <td class="chart-cell" data-type="DRY_FINES" data-element="${item.ELEMENT}">
                    ${item.DRY_FINES}
                </td>

                <td class="chart-cell" data-type="DRY_FINES_500TPH" data-element="${item.ELEMENT}">
                    ${item.DRY_FINES_500TPH}
                </td>
            </tr>`;
        });
    }

    $("#finesTable tbody").html(html);
}
function loadTrend(type, element) {
    $.ajax({
        url: '/RmbbPile/GetFinesTrend',
        type: 'GET',
        data: { type: type, element: element },
        success: function (res) {
            const modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();
            $("#modalTitle").text(element + " - " + type);

            setTimeout(function () {
                drawChart(res, element, type);
            }, 300);
        }
    });
}


function drawChart(data, element, type) {
    if (chartInstance != null) {
        chartInstance.dispose();
    }
    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({
        title: {
            text: element + " - " + type + " (30 Days Trend)",
            left: 'center'
        },
        tooltip: { trigger: 'axis' },
        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },
        yAxis: {
            type: 'value',
            name: type
        },
        series: [{
            name: element + " (" + type + ")",
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE),
            lineStyle: { width: 3 }
        }]
    });
}


    </script>
    }


</body>
</html>
