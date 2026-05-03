@{
    ViewBag.Title = ProcessTrends.App.PageTitle;
}

    @section css {
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
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

    <!-- MODAL -->
    <div class="modal fade" id="trendModal" tabindex="-1">
        <div class="modal-dialog modal-lg modal-dialog-centered">
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

@section scripts {    
 <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.plot.ly/plotly-2.30.0.min.js"></script>
   <script>

let chartInstance = null;

$(document).ready(function () {
    loadFinesData();
});

// CLICK CELL EVENT
$(document).on("click", ".chart-cell", function () {
    let type = $(this).data("type");
    loadTrend(type);
});

function loadFinesData() {

    $('#loader').show();

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesData',
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

            const modalEl = document.getElementById('trendModal');

            const modal = new bootstrap.Modal(modalEl);

            modal.show();

            // 🔥 IMPORTANT: wait until modal is fully visible
            setTimeout(function () {
                drawChart(res);
            }, 300);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}

function drawChart(data) {

    let xValues = data.map(x => x.DATE);
    let yValues = data.map(x => x.VALUE);

    let trace = {
        x: xValues,
        y: yValues,
        type: 'scatter',
        mode: 'lines+markers',
        line: {
            color: '#0d6efd',
            width: 3,
            shape: 'spline'
        }
    };

    let layout = {
        title: '30 Days Trend',
        xaxis: {
            title: 'Date'
        },
        yaxis: {
            title: 'Value'
        },
        margin: {
            t: 40
        }
    };

    Plotly.newPlot('trendChart', [trace], layout, { responsive: true });
}

</script>
}

