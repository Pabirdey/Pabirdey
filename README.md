@section css {
<link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
<link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">

<style>

body{
    background:#eef2f7;
}

/* Page Title */
.page-title{
    font-weight:700;
    color:#2c3e50;
}

/* Card */
.card-box{
    background:white;
    padding:25px 35px;
    border-radius:14px;
    box-shadow:0 6px 18px rgba(0,0,0,0.12);
}

/* ===== TABLE DESIGN ===== */
#materialTable{
    border-collapse:collapse;     /* Important for full border */
    width:100%;
}

/* Outer Border */
#materialTable{
    border:2px solid #333;
    border-radius:10px;
    overflow:hidden;
}

/* Header */
#materialTable thead{
    background:#1f4e79;
    color:white;
}

#materialTable th{
    font-size:20px;
    padding:10px;
    text-align:center;
}

/* Strong Inside Borders */
#materialTable th,
#materialTable td{
    border:2px solid #333 !important;
}

/* Row Text */
#materialTable td{
    font-size:20px;
    font-family:"Courier New";
    vertical-align:middle;
}

/* Hover */
#materialTable tbody tr:hover{
    background:#f5f7fa;
}

/* ===== COLUMN WIDTHS ===== */

/* Material Column Bigger */
#materialTable td:nth-child(1),
#materialTable th:nth-child(1){
    width:420px;
    font-weight:bold;
}

/* Value Tons */
#materialTable td:nth-child(2),
#materialTable th:nth-child(2){
    width:220px;
}

/* Value Kgs */
#materialTable td:nth-child(3),
#materialTable th:nth-child(3){
    width:240px;
}

/* Gap between Tons & Kgs */
#materialTable td:nth-child(3),
#materialTable th:nth-child(3){
    padding-left:35px;
}

/* Textboxes */
.medium-textbox{
    width:190px;
    height:50px;
    text-align:right;
    font-size:20px;
    font-weight:bold;
}

/* Buttons */
.btn-custom{
    padding-left:40px;
    padding-right:40px;
    font-size:18px;
    border-radius:8px;
}

</style>
}

<div class="app-content">
<div class="main-content">
<div class="container mt-5">

    <div class="card-box">

        <h3 class="text-center page-title mb-4">Raw Material Consumption</h3>

        <!-- Date + Furnace -->
        <div class="row mb-4">
            <div class="col-md-4">
                <label class="form-label fw-bold">Date</label><br>
                <a id="date-daily1" class="drpickr btn btn-primary">
                    <i class="fa fa-calendar"></i>
                    <label id="currDate-value" style="font-size:20px;color:white"></label>
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

        <!-- TABLE -->
        <table id="materialTable" class="table shadow-sm">
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
<script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
<script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>

<script>

$(document).ready(function () {

    var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",new System.Globalization.CultureInfo("en-GB"))';
    $('#currDate-value').html(caldate1);

    $('#date-daily1').datepicker({
        format:"dd/mm/yyyy",
        autoclose:true,
        todayHighlight:true
    }).datepicker("setDate", caldate1);

    $('#date-daily1').on('changeDate', function () {
        caldate1 = $('#date-daily1').datepicker('getFormattedDate');
        $('#currDate-value').html(caldate1);
        Display_Material($("#ddlFurnace").val(), caldate1);
    });

    $("#ddlFurnace").change(function () {
        Display_Material($("#ddlFurnace").val(), $('#date-daily1').datepicker('getFormattedDate'));
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
                        "<td>" + data[i].MATERIAL + "</td>" +
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

});

</script>
}