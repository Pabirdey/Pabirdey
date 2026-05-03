@{
    ViewBag.Title = ProcessTrends.App.PageTitle;
}

@section css {
<link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" />

<style>
    body {
        background: linear-gradient(to right, #eef2f7, #f8fbff);
        padding: 20px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .card {
        padding: 20px;
        border-radius: 15px;
        background: white;
        box-shadow: 0 8px 20px rgba(0,0,0,0.08);
        transition: 0.3s;
    }

    .card:hover {
        transform: translateY(-3px);
    }

    h3 {
        font-weight: 600;
        color: #0d47a1;
    }

    /* Loader */
    #loader {
        display: none;
        text-align: center;
        margin-bottom: 10px;
        font-weight: bold;
        color: #0d6efd;
    }

    /* Table */
    #finesTable {
        border-radius: 10px;
        overflow: hidden;
    }

    #finesTable thead {
        background: linear-gradient(to right, #0d47a1, #1976d2);
        color: white;
    }

    #finesTable th {
        padding: 12px;
        font-size: 14px;
        border: none;
    }

    #finesTable td {
        padding: 10px;
        font-size: 13px;
        border: none;
        transition: 0.2s;
    }

    /* Zebra rows */
    #finesTable tbody tr:nth-child(even) {
        background: #f4f7fb;
    }

    /* Hover */
    #finesTable tbody tr:hover {
        background: #e3f2fd;
        transform: scale(1.01);
    }

    #finesTable tbody tr {
        transition: all 0.2s ease-in-out;
    }

    .text-danger {
        font-weight: bold;
    }
</style>
}

<div class="app-content">

    @Html.Partial("_Header")

    <div class="main-content">
        <div class="container">

            <div class="card">

                <h3 class="text-center mb-3">📊 Pile Mat Wise Quality Data</h3>

                <div id="loader">
                    <span class="spinner-border spinner-border-sm"></span> Loading data...
                </div>

                <table class="table text-center" id="finesTable">
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
    </div>

</div>

@section scripts {

<script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
<script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.bundle.min.js")"></script>

<script>

    $(document).ready(function () {
        loadFinesData();
    });

    // 🔥 Load Data
    function loadFinesData() {

        $('#loader').show();

        $.ajax({
            url: '/Ore_Beneficiation/GetFinesData',
            type: 'GET',
            dataType: 'json',

            success: function (res) {

                console.log("API:", res);

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

    // 🔥 Show Error
    function showError(msg) {
        $('#finesTable tbody').html(
            `<tr><td colspan="5" class="text-danger">${msg}</td></tr>`
        );
    }

    // 🔥 Null Handle
    function getValue(val) {
        if (val === null || val === undefined || val === "" || val === "null") {
            return '-';
        }
        return val;
    }

    // 🔥 Render Table
    function renderTable(data) {

        let html = '';

        if (!data || data.length === 0) {
            html = "<tr><td colspan='5'>No data found</td></tr>";
        }
        else {

            data.forEach(function (item) {

                html += `
                    <tr>
                        <td>${getValue(item.ELEMENT)}</td>
                        <td>${getValue(item.RETURN_FINES)}</td>
                        <td>${getValue(item.WET_FINES)}</td>
                        <td>${getValue(item.DRY_FINES)}</td>
                        <td>${getValue(item.DRY_FINES_500TPH)}</td>
                    </tr>
                `;
            });
        }

        $('#finesTable tbody').html(html);
    }

</script>
}
