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
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        /* Page Layout Using Flexbox */
        .page-container {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .page-title {
            font-weight: 700;
            color: #2c3e50;
            text-align: center;
        }

        /* Top Section Flex */
        .top-section {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }

        .flex-box {
            flex: 1;
            min-width: 250px;
        }

        fieldset {
            border: 2px solid #2c3e50;
            padding: 15px;
            border-radius: 8px;
        }

        legend {
            font-size: 14px;
            font-weight: bold;
            padding: 0 10px;
            color: #2c3e50;
        }

        /* Table */
        #materialTable {
            width: 60%;
            margin: auto;
            background: white;
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
            font-size: 15px;
        }

        .medium-textbox {
            width: 100px;
            text-align: right;
            font-weight: bold;
        }

        /* Buttons */
        .button-section {
            display: flex;
            justify-content: center;
            gap: 20px;
        }

        .btn-custom {
            padding: 10px 40px;
            font-size: 15px;
            border-radius: 8px;
        }
    </style>
}

<div class="Main">
    <div class="page-container">

        <h2 class="page-title">Raw Material Consumption</h2>

        <!-- FLEXBOX TOP SECTION -->
        <div class="top-section">

            <!-- DATE -->
            <div class="flex-box">
                <fieldset>
                    <legend>Date Selection</legend>
                    <label>Date</label><br />
                    <a id="date-daily" class="btn btn-primary">
                        <span id="currDate-value"></span>
                    </a>
                </fieldset>
            </div>

            <!-- FURNACE -->
            <div class="flex-box">
                <fieldset>
                    <legend>Furnace Selection</legend>
                    <label>Furnace</label>
                    <select class="form-select" id="ddlFurnace">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </fieldset>
            </div>

        </div>

        <!-- TABLE -->
        <table id="materialTable" class="table table-bordered">
            <thead>
                <tr>
                    <th>Material</th>
                    <th>Value (Tons)</th>
                    <th>Value (Kgs)</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>

        <!-- BUTTONS -->
        <div class="button-section">
            <button class="btn btn-primary btn-custom" onclick="SaveBFRawMaterialCons()">Save</button>
            <button class="btn btn-secondary btn-custom">Back</button>
        </div>

    </div>
</div>

@section scripts {
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>

<script>
    var lsSelectedFDate = '';

    $(document).ready(function () {

        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
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
            url: '@Url.Action("GetBFRawMaterialByFurnace", "HML")',
            type: 'GET',
            data: { furnace: furnace, fdate: fDate },
            success: function (data) {

                var tbody = $("#materialTable tbody");
                tbody.empty();

                for (var i = 0; i < data.length; i++) {

                    tbody.append(
                        "<tr data-tagid='" + data[i].TAG_ID + "'>" +
                        "<td>" + data[i].MATERIAL + "</td>" +
                        "<td><input class='ton form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                        "<td><input class='kg form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                        "</tr>"
                    );
                }
            }
        });
    }

    function SaveBFRawMaterialCons() {

        var materials = [];
        var rows = document.querySelectorAll("#materialTable tbody tr");

        for (var i = 0; i < rows.length; i++) {

            var tagId = rows[i].getAttribute("data-tagid");
            var ton = rows[i].querySelector(".ton").value;
            var kg = rows[i].querySelector(".kg").value;

            materials.push({
                TAG_ID: tagId,
                VALUE_TON: ton,
                VALUE_KG: kg
            });
        }

        var data = {
            FDate: lsSelectedFDate,
            furnace: document.getElementById("ddlFurnace").value,
            materials: materials
        };

        $.ajax({
            url: '/HML/SaveBFRawMaterialData',
            type: 'POST',
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            data: JSON.stringify(data),
            success: function (res) {
                alert(res.message);
            },
            error: function () {
                alert("Error saving data");
            }
        });
    }
</script>
}
