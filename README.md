
@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" media="screen">
    <style>
        body {
            background-color: #f4f6f9;
        }

        .page-title {
            font-weight: 600;
            color: #2c3e50;
        }

        /*.card-box {
            background: #ffffff;
            padding: 20px;
            border-radius: 14px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.10);
            width: 700px;
            max-width: 90%;
            margin: 20px auto;
        }*/

        table {
            background: white;
            border-radius: 10px;
            overflow: hidden;
        }

        thead {
            font-size: 22px;
            font-family: Courier New, Courier, monospace;
            color: white;
        }

        td {
            font-family: 'Courier New';
            font-size: 22px;
        }

        .table tbody tr:hover {
            background: #f1f1f1;
        }

        .medium-textbox {
            width: 80px;
            max-width: 80px;
            text-align: right;
        }

        .btn-custom {
            padding-left: 35px;
            padding-right: 35px;
            font-size: 16px;
            border-radius: 8px;
        }

        input[type="text"] {
            font-weight: bold;
            font-size: 16px;
        }

        .medium-textbox {
            height: 50px !important;
            line-height: 1 !important;
            padding: 1px 4px;
            font-size: 22px;
            font-weight: bold;
        }

        table, td, th {
        }

        table {
            border-collapse: collapse;
        }
    </style>

}
<div class="app-content">
    @*@Html.Partial("_Header")*@
    <div class="main-content">
        <div class="container mt-5">
            <div class="card-box">
                <h3 class="text-center page-title margin-bottom-10">Raw Material Consumption</h3>
                <!-- Date & Furnace Row -->
                <div class="row margin-10">
                    <div class="col-md-4">
                        <label class="form-label">Date</label>
                        <a id="date-daily1" class="drpickr btn btn-o btn-primary">
                            <i class="fa fa-calendar"></i> <label class="value" id="currDate-value" style="font-size:20px;color:blue"></label>
                        </a>
                    </div>
                    <div class="col-md-3">
                        <label class="form-label fw-bold">Furnace</label>
                        <select class="form-select shadow-sm" id="ddlFurnace">
                            <option>C</option>
                            <option>E</option>
                            <option>F</option>
                        </select>
                    </div>
                </div>
                <!-- Table -->
                <div>
                    <table id="materialTable" class="table table-bordered shadow-sm" style="border:1px solid;padding: 10px;">
                        <thead>
                            <tr>
                                <th>Material</th>
                                <th>Value (Tons)</th>
                                <th>Value (Kgs)</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
                <!-- Buttons -->
                <div class="mt-4">
                    <button class="btn btn-primary btn-custom me-2">Save</button>
                    <button class="btn btn-secondary btn-custom">Back</button>
                </div>
            </div>
        </div>
    </div>

</div>
@section scripts {
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
    <script src="@Url.Content("~/bower_components/components-modernizr/modernizr.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script type="text/javascript">
    $(document).ready(function () {
        var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').html(caldate1);
        $('#date-daily1').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker("setDate", caldate1);

        $('#date-daily1').on('changeDate', function () {
            caldate1 = $('#date-daily1').datepicker('getFormattedDate');
            $('#currDate-value').html(caldate1);
            var furnace = $("#ddlFurnace").val();
            Display_Material(furnace, caldate1);
        });


        $("#ddlFurnace").change(function () {
            var furnace = $("#ddlFurnace").val();
            var fDate = $('#date-daily1').datepicker('getFormattedDate');
            Display_Material(furnace, fDate);
        });
        Display_Material($("#ddlFurnace").val(), caldate1);
        function Display_Material(furnace, fDate) {
            $.ajax({
                url: '@Url.Action("GetRawMaterialByFurnace","HML")',
                type: 'GET',
                data: { furnace: furnace, fdate: fDate },
                success: function (data) {
                    var tbody = $("#materialTable tbody");
                    tbody.empty();
                    for (var i = 0; i < data.length; i++) {
                        var row = "<tr>" +
                            "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                            "<td><input type='text' class='form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                            "<td><input type='text' class='form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                            "</tr>";
                        tbody.append(row);
                    }
                },
                error: function (xhr) {
                    alert("Error Occurred: " + xhr.responseText);
                }
            });
        }

    });
    </script>

}


