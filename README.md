 $(document).ready(function () {
        lsSelectedFDate = '@DateTime.Today.AddDays(0).ToString("dd-MMM-yyyy", new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').text(lsSelectedFDate);
        $('#hiddenDate').datepicker({
            format: "dd/mmm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', lsSelectedFDate);
        $('#tbFDatePick').on('click', function (e) {
            e.preventDefault();
            $('#hiddenDate').datepicker('show');
        });
        $('#hiddenDate').on('changeDate', function (e) {
            lsSelectedFDate = e.format('dd/mm/yyyy');
            $('#currDate-value').text(lsSelectedFDate);
            Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);

        });
        IsSelectedFur = $('#lstFur').val();
        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();
            Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);
        });
        Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);

    });
