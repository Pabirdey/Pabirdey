 $(document).ready(function () {

        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MMM/yyyy", new System.Globalization.CultureInfo("en-GB")).ToUpper()';

        $('#currDate-value').text(lsSelectedFDate);

        $('#hiddenDate').datepicker({
            format: "dd/M/yyyy",
            autoclose: true,
            todayHighlight: true
        });

        $('#hiddenDate').datepicker('setDate', new Date());

        $('#tbFDatePick').on('click', function (e) {

            e.preventDefault();

            $('#hiddenDate').datepicker('show');

        });

        $('#hiddenDate').on('changeDate', function (e) {

            let dt = e.date;

            let day = ("0" + dt.getDate()).slice(-2);

            let months = ["JAN", "FEB", "MAR", "APR", "MAY", "JUN",
                          "JUL", "AUG", "SEP", "OCT", "NOV", "DEC"];

            let month = months[dt.getMonth()];

            let year = dt.getFullYear();

            lsSelectedFDate = day + "/" + month + "/" + year;

            $('#currDate-value').text(lsSelectedFDate);

            Dis_GBF_TO_IBF_ReportData(lsSelectedFDate);

        });

        Dis_GBF_TO_IBF_ReportData(lsSelectedFDate);

    });
