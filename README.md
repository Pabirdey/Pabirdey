let lsSelectedFDate;

$(document).ready(function () {

    var now = new Date();
    var hour = now.getHours();

    $("#ddlshift").val(
        hour >= 22 || hour < 6 ? "C" :
        hour >= 14 ? "B" : "A"
    );

    if (hour < 6)
        now.setDate(now.getDate() - 1);

    // Set selected date
    lsSelectedFDate = now.toLocaleDateString('en-GB');

    $("#currDate-value").text(lsSelectedFDate);

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
        lsSelectedFDate = e.format('dd/MM/yyyy');
        $('#currDate-value').text(lsSelectedFDate);

        Display_Granshot_Details();
        DisplayProductionSummary();
    });

    $('#ddlshift').on('change', function () {
        Display_Granshot_Details();
        DisplayProductionSummary();
    });

    Display_Granshot_Details();
    DisplayProductionSummary();
});
