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

        /* ===== FLEXBOX FOR TABLES ===== */

        .Consumption {
            display: flex;
            gap: 20px;
            align-items: flex-start;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        #materialTable {
            flex: 2;
            min-width: 50px;
            background: white;
        }

        #types {
            flex: 1;
            min-width: 250px;
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

        #types th {
            background: #34495e;
            color: white;
            text-align: center;
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
        .types tr{
            display:none;
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
                    <a id="date-daily" class="btn btn-primary">
                        <span id="currDate-value"></span>
                    </a>
                </fieldset>
            </div>
            <!-- FURNACE -->
            <div class="col-md-3">
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
        <!-- FLEX TABLE SECTION -->
        <div class="Consumption">
            <!-- MATERIAL TABLE -->
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
            <!-- TYPES TABLE -->
            <table id="types" class="table table-bordered">
                <thead>
                    <tr>
                        <th>Types</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>
                            <select id="ddlCoal" class="form-select">
                                <option value=""></option>
                                <option value="IPC">IPC</option>
                                <option value="RPC">RPC</option>
                                <option value="Curragh(N)+Aunthra">Curragh(N)+Aunthra</option>
                                <option value="West Bokaro">West Bokaro</option>
                                <option value="Jellinbah">Jellinbah</option>
                                <option value="Foxleigh">Foxleigh</option>
                            </select>
                        </td>                        
                    </tr>
                    <tr>
                        <td>
                            <select id="ddlIO" class="form-select">
                                <option value=""></option>
                                <option value="BF Sized Banspani">BF Sized Banspani</option>
                                <option value="BF Sized Joda">BF Sized Joda</option>
                                <option value="BF Sized Khondbond">BF Sized Khondbond</option>
                                <option value="BF Sized Noamundi">BF Sized Noamundi</option>
                                <option value="LD Sized Noamundi">LD Sized Noamundi</option>                                
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <select id="ddlPyro" class="form-select">
                                <option value=""></option>
                                <option value="Sukinda">Sukinda</option>
                                <option value="Local">Local</option>                                
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <select id="ddlLimestone" class="form-select">
                                <option value=""></option>
                                <option value="Gotan">Gotan</option>
                                <option value="SP Grade">SP Grade</option>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                           <label style="font-family:Courier New, Courier, monospace;font-weight:bold;font-size:15px;"><strong>Theoretical Production</strong></label><br />
                            <input type="text" />
                        </td>
                    </tr>
                </tbody>                
            </table>
        </div>
        <!-- BUTTONS -->
        <div class="text-center mt-4">
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
            contentType: 'application/json',
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
