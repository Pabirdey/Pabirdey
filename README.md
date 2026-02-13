@{
    ViewBag.Title = "Raw Material Consumption";
}

@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">

    <style>
        body {
            background-color: #f4f6f9;
        }

        .Main {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
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
            margin-top: 20px;
        }

        #materialTable th {
            background: #2c3e50;
            color: white;
            text-align: center;
            font-size: 16px;
        }

        #materialTable td {
            border: 1px solid #000;
            font-weight: bold;
            font-size: 14px;
        }

        .medium-textbox {
            width: 120px;
            text-align: right;
            font-weight: bold;
        }

        .btn-custom {
            padding: 8px 30px;
            font-size: 14px;
            border-radius: 8px;
        }
    </style>
}

<div class="container mt-4">
    <div class="Main">

        <h3 class="text-center page-title mb-4">Raw Material Consumption</h3>

        <div class="row">

            <!-- DATE -->
            <div class="col-md-3">
                <fieldset>
                    <legend>Date Selection</legend>

                    <label>Date</label>
                    <div id="date-daily" class="btn btn-primary w-100">
                        <i class="glyphicon glyphicon-calendar"></i>
                        <span id="currDate-value"></span>
                    </div>

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
        <div class="row">
            <div class="col-md-12">

                <table id="materialTable" class="table table-bordered">
                    <thead>
                        <tr>
                            <th style="width:40%">Material</th>
                            <th style="width:30%">Value (Tons)</th>
                            <th style="width:30%">Value (Kgs)</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>

            </div>
        </div>

        <!-- BUTTONS -->
        <div class="text-center mt-4">
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

    var selectedDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy")';
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

            var tbody = $("#materialTable tbody");
            tbody.empty();

            for (var i = 0; i < data.length; i++) {

                tbody.append(
                    "<tr>" +
                    "<td class='material'>" + data[i].MATERIAL + "</td>" +
                    "<td><input type='number' step='0.001' class='ton form-control medium-textbox' value='" + (data[i].VALUE_TON || 0) + "'></td>" +
                    "<td><input type='number' step='0.01' class='kg form-control medium-textbox' value='" + (data[i].VALUE_KG || 0) + "'></td>" +
                    "</tr>"
                );
            }
        }
    });
}


// AUTO CALCULATE KG WHEN TON CHANGES
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

    $("#materialTable tbody tr").each(function () {

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
        success: function (response) {
            alert("Data Saved Successfully!");
        },
        error: function () {
            alert("Error while saving data.");
        }
    });
}

</script>
}