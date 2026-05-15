let lsSelectedFDate;
        let IsSelectedFur;
        $(document).ready(function () {
            lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MMM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            $('#currDate-value').text(lsSelectedFDate);
            $('#hiddenDate').datepicker({
                format: "dd/MMM/yyyy",
                autoclose: true,
                todayHighlight: true
            }).datepicker('setDate', lsSelectedFDate);
            $('#tbFDatePick').on('click', function (e) {
                e.preventDefault();
                $('#hiddenDate').datepicker('show');
            });
            $('#hiddenDate').on('changeDate', function (e) {
                lsSelectedFDate = e.format('dd/MMM/yyyy');
                $('#currDate-value').text(lsSelectedFDate);
                Dis_GBF_TO_IBF_ReportData(lsSelectedFDate);
            });
            Dis_GBF_TO_IBF_ReportData(lsSelectedFDate);
