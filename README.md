@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">
    <style>
        .Main
        {
            background-color:#ffffff;
        }
        .page-title {
            font-weight: 700;
            color: #2c3e50;
        }

        fieldset {
            border: 2px solid #2c3e50;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }

        legend {
            font-size: 14px;
            font-weight: bold;
            padding: 0 10px;
            color: #2c3e50;
        }

        #materialTable {
            width: 45%;
            background: white;
            color: #000;
        }

            #materialTable th {
                background: #2c3e50;
                color: white;
                text-align: center;
                font-family: Courier New;
                font-size:18px;
            }

            #materialTable td {
                border: 1px solid #000;
                font-family: Courier New, Courier, monospace;
                font-weight: bold;
                font-size:16px;
            }

        .medium-textbox {
            width: 100px;
            text-align: right;
            font-weight: bold;
        }

        .btn-custom {
            padding: 10px 40px;
            font-size: 15px;
            border-radius: 8px;
        }
    </style>
}
<div class="Main">
    <div class="container">
        <h2 class="text-center page-title mb-4">Raw Material Consumption</h2>
        <div class="row">
            <!-- DATE FIELDSET -->
            <div class="col-md-2">
                <fieldset>
                    <legend>Date Selection</legend>
                    <label class="fw-bold">Date</label><br />
                    <a id="date-daily" class="btn btn-primary">
                        <i class="fa fa-calendar"></i>
                        <span id="currDate-value"></span>
                    </a>
                </fieldset>
            </div>
            <!-- FURNACE FIELDSET -->
            <div class="col-md-2">
                <fieldset>
                    <legend>Furnace Selection</legend>
                    <label class="fw-bold">Furnace</label>
                    <select class="form-select" id="ddlFurnace">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </fieldset>
            </div>
        </div>
        <!-- TABLE For Consumption-->
        <table id="materialTable" class="table table-bordered mt-3">
            <thead>
                <tr>
                    <th>Material</th>
                    <th>Value (Tons)</th>
                    <th>Value (Kgs)</th>                    
                </tr>
            </thead>                     
            <tbody></tbody>
            <thead>
                <tr>
                    <th>Types.</th>
                </tr>
            </thead>          
        </table>      

        <!-- BUTTONS -->
        <div class="mt-4">
            <button class="btn btn-primary btn-custom" onclick="SaveRawMaterialData()">Save</button>
            <button class="btn btn-secondary btn-custom">Back</button>
        </div>
    </div>
</div>
@section scripts {
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script>
$(document).ready(function () {
    var lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
    $('#currDate-value').text(lsSelectedFDate);
    $('#date-daily').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    }).datepicker("setDate", lsSelectedFDate);
    $('#date-daily').on('changeDate', function () {
        lsSelectedFDate = $('#date-daily').datepicker('getFormattedDate');
        $('#currDate-value').text(lsSelectedFDate);
        Display_Material($('#ddlFurnace').val(), lsSelectedFDate);
    });

    $('#ddlFurnace').change(function () {
        Display_Material($(this).val(), lsSelectedFDate);
    });

    Display_Material($('#ddlFurnace').val(), lsSelectedFDate);
});

function Display_Material(furnace, fDate) {
    $.ajax({
        url: '@Url.Action("GetRawMaterialByFurnace","HML")',
        type: 'GET',
        data: { furnace: furnace, fdate: fDate },
        success: function (data) {
            var tbody = $("#materialTable tbody");
            tbody.empty();
            for (var i = 0; i < data.length; i++) {
                tbody.append("<tr>" +
                    "<td class='material'>" + data[i].MATERIAL + "</td>" +
                    "<td><input class='ton form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                    "<td><input class='kg form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                    "</tr>"
                );
            }
        }
    });
}       
    </script>
}
