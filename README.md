@{
    ViewBag.Title = "Cast House Details";
    Layout = null;
}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Bootstrap Datepicker -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">

    <!-- Font Awesome -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">

    <!-- 🔧 REQUIRED FIX FOR MONTH / YEAR HEADING -->
    <style>
        .datepicker {
            z-index: 1055 !important;
        }

        .datepicker-days table thead tr:first-child {
            height: 40px;
        }

        .datepicker-days table thead th {
            line-height: 30px !important;
            padding: 5px 10px !important;
            font-weight: bold;
        }

        .datepicker table tr td,
        .datepicker table tr th {
            width: 32px;
            height: 32px;
        }
    </style>
</head>

<body>

<div class="container mt-4">

    <!-- DATE + FURNACE -->
    <div class="mb-3">

        <!-- DATE BUTTON -->
        <a id="tbFDatePick" class="btn btn-primary">
            <i class="fa fa-calendar"></i>
            <label id="currDate-value" style="font-size:12px;color:white"></label>
        </a>

        <!-- HIDDEN INPUT -->
        <input type="text" id="hiddenDate"
               style="position:absolute; opacity:0; height:0; width:0;" />

        &nbsp;&nbsp;

        <!-- FURNACE -->
        <label class="fw-bold">Furnace</label>
        <select id="lstFur" class="form-select d-inline-block w-auto">
            <option value="C">C</option>
            <option value="D">D</option>
            <option value="E">E</option>
            <option value="F">F</option>
        </select>
    </div>

    <!-- TABLE -->
    <table class="table table-bordered" id="TAP_Hot_Metal_Details">
        <thead class="table-light">
            <tr>
                <th>Cast No</th>
                <th>Trough No</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

</div>

<!-- jQuery -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<!-- Datepicker JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

<script>
    let lsSelectedFDate;
    let IsSelectedFur;

    $(document).ready(function () {

        // Default date = yesterday
        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').text(lsSelectedFDate);

        // Furnace default
        IsSelectedFur = $('#lstFur').val();

        // Datepicker init
        $('#hiddenDate').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', lsSelectedFDate);

        // Button click → open calendar
        $('#tbFDatePick').on('click', function (e) {
            e.preventDefault();
            $('#hiddenDate').datepicker('show');
        });

        // Date change
        $('#hiddenDate').on('changeDate', function (e) {
            lsSelectedFDate = e.format('dd/mm/yyyy');
            $('#currDate-value').text(lsSelectedFDate);
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });

        // Furnace change
        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });

        // Initial load
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
    });

    // SAMPLE FUNCTION
    function Display_Tap_Hole_Details(Fdate, Fur) {

        console.log("Date:", Fdate, "Furnace:", Fur);

        let html = `
            <tr>
                <td>101</td>
                <td>A</td>
            </tr>`;

        $('#TAP_Hot_Metal_Details tbody').html(html);
    }
</script>

</body>
</html>