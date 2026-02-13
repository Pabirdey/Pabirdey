@{
    ViewBag.Title = "Raw Material Consumption";
}

@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">

    <style>
        .Main {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
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
            width: 60%;
            background: white;
            color: #000;
        }

        #materialTable th {
            background: #2c3e50;
            color: white;
            text-align: center;
            font-family: Courier New;
            font-size: 16px;
        }

        #materialTable td {
            border: 1px solid #000;
            font-family: Courier New, monospace;
            font-weight: bold;
            font-size: 14px;
        }

        .medium-textbox {
            width: 110px;
            text-align: right;
            font-weight: bold;
        }

        .section-header {
            background: #dfe6e9;
            font-weight: bold;
            text-align: left;
        }

        .btn-custom {
            padding: 8px 30px;
            font-size: 14px;
            border-radius: 6px;
        }
    </style>
}

<div class="Main">
    <div class="container">

        <h2 class="text-center page-title mb-4">Raw Material Consumption</h2>

        <div class="row">

            <!-- DATE -->
            <div class="col-md-3">
                <fieldset>
                    <legend>Date Selection</legend>
                    <label>Date</label><br />
                    <a id="date-daily" class="btn btn-primary w-100">
                        <span id="currDate-value"></span>
                    </a>
                </fieldset>
            </div>

            <!-- FURNACE -->
            <div class="col-md-3">
                <fieldset>
                    <legend>Furnace Selection</legend>
                    <label>Furnace</label>
                    <select class="form-control" id="ddlFurnace">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </fieldset>
            </div>

        </div>

        <!-- TABLE -->
        <table id="materialTable" class="table table-bordered mt-3">

            <thead>
                <tr>
                    <th>Material</th>
                    <th>Value (Tons)</th>
                    <th>Value (Kgs)</th>
                </tr>
            </thead>

            <tbody>

                <!-- TYPES HEADER -->
                <tr>
                    <td colspan="3" class="section-header">
                        Types - Consumption
                    </td>
                </tr>

            </tbody>

            <tbody id="consumptionBody">
                <!-- AJAX DATA WILL LOAD HERE -->
            </tbody>

        </table>

        <!-- BUTTONS -->
        <div class="mt-4">
            <button class="btn btn-success btn-custom" onclick="SaveRawMaterialData()">Save</button>
            <button class="btn btn-secondary btn-custom" onclick="history.back()">Back</button>
        </div>

    </div>
</div>

@section scripts {

<script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
<script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
<script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>

<script>

$(document).ready(function () {

    var selectedDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

    $('#currDate-value').text(selectedDate);

    $('#date-daily').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    }).datepicker("setDate", selectedDate);

    $('#date-daily').on('changeDate', function () {
        selectedDate = $('#date-daily').datepicker('getFormattedDate');
        $('#currDate-value').text(selectedDate);
        Display_Material($('#ddlFurnace').val(), selectedDate);
    });

    $('#ddlFurnace').change(function () {
        Display_Material($(this).val(), selectedDate);
    });

    Display_Material($('#ddlFurnace').val(), selectedDate);
});


function Display_Material(furnace, fDate) {

    $.ajax({
        url: '@Url.Action("GetRawMaterialByFurnace","HML")',
        type: 'GET',
        data: { furnace: furnace, fdate: fDate },

        success: function (data) {

            var tbody = $("#consumptionBody");
            tbody.empty();

            for (var i = 0; i < data.length; i++) {

                tbody.append("<tr>" +
                    "<td class='material'>" + data[i].MATERIAL + "</td>" +
                    "<td><input type='number' step='0.001' class='ton form-control medium-textbox' value='" + (data[i].VALUE_TON || 0) + "'></td>" +
                    "<td><input type='number' step='0.01' class='kg form-control medium-textbox' value='" + (data[i].VALUE_KG || 0) + "'></td>" +
                    "</tr>"
                );
            }
        }
    });
}


// AUTO CALCULATE KG
$(document).on('input', '.ton', function () {
    var ton = parseFloat($(this).val()) || 0;
    var kg = ton * 1000;
    $(this).closest('tr').find('.kg').val(kg.toFixed(2));
});


// SAVE FUNCTION
function SaveRawMaterialData() {

    var dataList = [];
    var selectedDate = $('#currDate-value').text();
    var furnace = $('#ddlFurnace').val();

    $("#consumptionBody tr").each(function () {

        var material = $(this).find('.material').text();
        var ton = $(this).find('.ton').val();
        var kg = $(this).find('.kg').val();

        dataList.push({
            FDATE: selectedDate,
            FURNACE: furnace,
            MATERIAL: material,
            VALUE_TON: ton,
            VALUE_KG: kg
        });
    });

    $.ajax({
        url: '@Url.Action("SaveRawMaterial","HML")',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(dataList),

        success: function () {
            alert("Data Saved Successfully!");
        },

        error: function () {
            alert("Error while saving data.");
        }
    });
}

</script>
}