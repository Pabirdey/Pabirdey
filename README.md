let lsSelectedFDate;
        let IsSelectedFur;
            $(document).ready(function() {
                let lsSelectedFDate;
                let IsSelectedFur;
                lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

    $('#currDate-value').text(lsSelectedFDate);
    // Attach datepicker to hidden input
    $('#hiddenDate').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    }).datepicker("setDate", lsSelectedFDate);

    // Open datepicker when button clicked
    $('#tbFDatePick').on('click', function () {
        $('#hiddenDate').datepicker('show');
    });

    // Correct changeDate handler
    $('#hiddenDate').on('changeDate', function (e) {
        lsSelectedFDate = e.format('dd/mm/yyyy');
        $('#currDate-value').text(lsSelectedFDate);
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
    });

    IsSelectedFur = $('#lstFur').val();
    Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);

    $('#lstFur').change(function () {
        IsSelectedFur = $(this).val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
    });
            });
            <a id="tbFDatePick" class="drpickr btn btn-primary">
                <i class="fa fa-calendar"></i>
                <label id="currDate-value" style="font-size:12px;color:white"></label>
            </a>
