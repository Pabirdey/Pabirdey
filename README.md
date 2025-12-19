<a id="date-daily1" class="drpickr btn btn-o btn-primary">
    <i class="fa fa-calendar"></i>
    <label class="value" id="currDate-value" style="font-size:20px;color:blue"></label>
</a>

<input type="text" id="From_datepicker" class="d-none" />


<script src="~/Bootstrap5/jquery-3.7.1.js"></script>
<script src="~/Bootstrap5/bootstrap.js"></script>
<script src="~/Bootstrap5/bootstrap-datepicker.js"></script>
<link href="~/Bootstrap5/bootstrap-datepicker.css" rel="stylesheet" />



<script type="text/javascript">
    let lsSelectedFDate;

    $(document).ready(function () {

        // Default date = Yesterday
        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
        $("#currDate-value").text(lsSelectedFDate);

        // Initialize datepicker
        $("#From_datepicker").datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker("setDate", lsSelectedFDate);

        // Open datepicker on button click
        $("#date-daily1").click(function () {
            $("#From_datepicker").datepicker("show");
        });

        // On date change
        $("#From_datepicker").on("changeDate", function (e) {
            lsSelectedFDate = e.format("dd/mm/yyyy");
            $("#currDate-value").text(lsSelectedFDate);

            // call your method here if needed
            // loadMaterials(selectedFurnace, lsSelectedFDate);
        });
    });
</script>