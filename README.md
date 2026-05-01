 $(document).ready(function () {
            lsSelectedFDate = '@DateTime.Today.AddDays(-2).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            $('#currDate-value').text(lsSelectedFDate);
            $('#hiddenDate').datepicker({
                format: "dd/mm/yyyy",
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
                Display_Bin_Position();
            });
            Display_Bin_Position();
        });
