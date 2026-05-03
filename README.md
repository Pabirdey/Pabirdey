@{
    ViewBag.Title = ProcessTrends.App.PageTitle;
}

@section css {
<link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" />

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

    @Html.Partial("_Header")

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

    <!-- ✅ REQUIRED LIBRARIES -->
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>

    <script>

        $(document).ready(function () {
            loadFinesData();
        });

        // ✅ LOAD DATA FROM CONTROLLER
        function loadFinesData() {

            $('#loader').show();

            $.ajax({
                url: '/Ore_Beneficiation/GetFinesData',
                type: 'GET',
                dataType: 'json',

                success: function (res) {

                    console.log("API Response:", res);

                    // CASE 1: error
                    if (res && res.error) {
                        showError(res.error);
                    }

                    // CASE 2: { success, data }
                    else if (res && res.data) {
                        renderTable(res.data);
                    }

                    // CASE 3: direct array
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

        // ✅ SHOW ERROR
        function showError(msg) {
            $('#finesTable tbody').html(
                `<tr><td colspan="5" class="text-danger">${msg}</td></tr>`
            );
        }

        // ✅ HANDLE NULL VALUES
        function getValue(val) {
            if (val === null || val === undefined || val === "" || val === "null") {
                return '-';
            }
            return val;
        }

        // ✅ RENDER TABLE
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
