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

<!-- ✅ BOOTSTRAP 5 MODAL -->
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
