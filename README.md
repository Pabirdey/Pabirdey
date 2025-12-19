<script type="text/javascript">
    let lsSelectedFDate;

    $(document).ready(function () {

        // Yesterday date
        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

        // Show default date
        $("#currDate-value").text(lsSelectedFDate);

        // Init datepicker
        $("#From_datepicker").datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        });

        // Set default date
        $("#From_datepicker").datepicker("setDate", lsSelectedFDate);

        // 🔹 Open datepicker on button click
        $("#date-daily1").click(function () {
            $("#From_datepicker").datepicker("show");
        });

        // 🔹 Date change event
        $("#From_datepicker").on("changeDate", function (e) {
            lsSelectedFDate = e.format("dd/mm/yyyy");
            $("#currDate-value").text(lsSelectedFDate);
        });

    });
</script>