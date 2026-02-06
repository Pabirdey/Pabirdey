@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">
    <style>      

        /* Header */
        .page-title {
            font-weight: 700;
            color: #2c3e50;
        }
               
        /* TABLE */
        #materialTable {
            border-collapse: collapse;
            width: 45%;
            background: white;
            color:#000000;
        }

            #materialTable thead {                
                color:#000000  ;             
            }

            #materialTable th {
                font-size: 16px;
                padding: 14px;
                text-align: center;
                font-family: Courier New, Courier, monospace;
                font-weight: bold;
                color:#ffffff;
            }

            #materialTable td {
                font-size: 16px;
                font-family: Courier New, Courier, monospace;
                padding: 10px;
                vertical-align: middle;
                border: 2px solid #000;
                font-weight: bold;
                color:#000;
            }

            #materialTable th,
            #materialTable td {
                border: 1px solid black;
            }

            #materialTable tbody tr:hover {
                background: #f5f7fa;
            }

            /* -------- COLUMN WIDTH BIG -------- */

            /* MATERIAL COLUMN BIG */
            #materialTable th:nth-child(1),
            #materialTable td:nth-child(1) {
                width: 120px;
            }

            /* VALUE (TONS) COLUMN BIG */
            #materialTable th:nth-child(2),
            #materialTable td:nth-child(2) {
                width: 150px;
                text-align: center;
            }

            /* VALUE (KGS) COLUMN BIG */
            #materialTable th:nth-child(3),
            #materialTable td:nth-child(3) {
                width: 150px;
                text-align: center;
            }

        /* -------- INPUT SIZE -------- */
        .medium-textbox {
            width: 100px;
            height: 40px;
            text-align: right;
            font-size: 15px;
            font-weight: bold;
        }

        /* Buttons */
        .btn-custom {
            padding-left: 40px;
            padding-right: 40px;
            font-size: 15px;
            border-radius: 8px;
        }
    </style>
}
<div class="Main" style="background-color:#ffffff">
    <div class="container mt-10">
        <div>
            <h2 class="text-center page-title mb-4">Raw Material Consumption</h2>
            <!-- Date + Furnace -->
            <div class="row mb-4">
                <div class="col-md-4">
                    <label class="form-label fw-bold">Date</label>
                    <a id="date-daily" class="drpickr btn btn-primary">
                        <i class="fa fa-calendar"></i>
                        <label id="currDate-value" style="font-size:12px;color:white"></label>
                    </a>
                    <label class="form-label fw-bold">Furnace</label>
                    <select class="form-select shadow-sm" id="ddlFurnace">
                        <option>C</option>
                        <option>E</option>
                        <option>F</option>
                    </select>
                </div>
                <div class="col-md-4">
                    <label class="form-label fw-bold">Types</label>
                </div>
            </div>
            <!-- TABLE -->
            <div style="margin-top:20px;">
                <table id="materialTable" class="table table-bordered shadow-sm">
                    <thead>
                        <tr>
                            <th class="material">Material</th>
                            <th class="ton">Value(Tons)</th>
                            <th class="kg">Value(Kgs)</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
            <!-- BUTTONS -->
            <div class="mt-4">
                <button class="btn btn-primary btn-custom me-2 btnSaveMaterial" onclick="SaveRawMaterialData()">Save</button>
                <button class="btn btn-secondary btn-custom">Back</button>
            </div>
        </div>
    </div>
</div>
@section scripts {
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>
    <script>
    $(document).ready(function () {
             var lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",new System.Globalization.CultureInfo("en-GB"))';
                 $('#currDate-value').html(lsSelectedFDate);
                 $('#date-daily').datepicker({
                    format:"dd/mm/yyyy",
                    autoclose:true,
                    todayHighlight:true
                }).datepicker("setDate", lsSelectedFDate);

            $('#date-daily').on('changeDate', function () {
                lsSelectedFDate = $('#date-daily').datepicker('getFormattedDate');
                $('#currDate-value').html(lsSelectedFDate);
                Display_Material($("#ddlFurnace").val(), lsSelectedFDate);
            });

            $("#ddlFurnace").change(function () {
                Display_Material($("#ddlFurnace").val(),
                $('#date-daily').datepicker('getFormattedDate'));
            });

            Display_Material($("#ddlFurnace").val(), lsSelectedFDate);
            $(document).ready(function () {
                $('.btnSaveMaterial').on('click', function () {
                    SaveRawMaterialData();
                });
            });

            function SaveRawMaterialData() {
                debugger;
                let furnace = document.getElementById("txtFurnace").value;
                let selectedDate = document.getElementById("txtDate").value;
                let rows = [];
                let tableRows = document.querySelectorAll("#materialTable tbody tr");
                tableRows.forEach(function (row) {
                    rows.push({
                        furnace: furnace,
                        material: row.querySelector(".material").textContent.trim(),
                        date: selectedDate,
                        valueTon: row.querySelector(".ton").value,
                        valueKg: row.querySelector(".kg").value
                    });
                });
            }

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
                alert('Error: ' + xhr.responseText);
            }
        });
    }
        function SaveRawMaterialData() {
            debugger;
            let furnace = document.getElementById("ddlFurnace").value;
            let selectedDate = document.getElementById("lsSelectedFDate");
            let rows = [];
            let tableRows = document.querySelectorAll("#materialTable tbody tr");
                tableRows.forEach(function(row) {
                    rows.push({
                    furnace: furnace,
                    material: row.querySelector(".material").textContent.trim(),
                    date: selectedDate,
                    valueTon: row.querySelector(".ton").value,
                    valueKg: row.querySelector(".kg").value
                });
            });      
}

});
    </script>
}
