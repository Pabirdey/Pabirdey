@{
    ViewBag.Title = "Cast House Details";
    Layout = null;
}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Bootstrap Datepicker -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">

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

        <!-- HIDDEN INPUT (REQUIRED) -->
        <input type="text" id="hiddenDate"
               style="position:absolute; opacity:0; height:0; width:0;" />

        &nbsp;&nbsp;

        <!-- FURNACE -->
        <label class="fw-bold">Furnace</label>
        <select id="lstFur">
            <option value="C">C</option>
            <option value="D">D</option>
            <option value="E">E</option>
            <option value="F">F</option>
        </select>
    </div>

    <!-- TABLE (SAMPLE) -->
    <table class="table table-bordered" id="TAP_Hot_Metal_Details">
        <thead>
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

<!-- Bootstrap -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<!-- Datepicker -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

<script>
    let lsSelectedFDate;
    let IsSelectedFur;

    $(document).ready(function () {

        // Default date = yesterday
        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

        $('#currDate-value').text(lsSelectedFDate);

        // Init datepicker on hidden input
        $('#hiddenDate').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', lsSelectedFDate);

        // Open calendar on button click
        $('#tbFDatePick').on('click', function (e) {
            e.preventDefault();
            $('#hiddenDate').datepicker('show');
        });

        // Date change event
        $('#hiddenDate').on('changeDate', function (e) {
            lsSelectedFDate = e.format('dd/mm/yyyy');
            $('#currDate-value').text(lsSelectedFDate);
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });

        // Furnace
        IsSelectedFur = $('#lstFur').val();

        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });

        // Initial load
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
    });

    // SAMPLE AJAX FUNCTION
    function Display_Tap_Hole_Details(Fdate, Fur) {

        console.log("Date:", Fdate, "Furnace:", Fur);

        // Example static data (replace with AJAX)
        let html = `
            <tr>
                <td>101</td>
                <td>A</td>
            </tr>`;

        $('#TAP_Hot_Metal_Details tbody').html(html);

        /*
        $.ajax({
            url: '/CastHouse/Get_TAP_Hole_Metal_Details',
            type: 'GET',
            data: { Fdate: Fdate, Fur: Fur },
            success: function (res) {
                // bind table
            }
        });
        */
    }
</script>

</body>
</html>