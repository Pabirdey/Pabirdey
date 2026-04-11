<script>
function loadData() {

    var date = $("#txtDate").val();
    var formattedDate = date.replace("T", " ") + ":00";

    $.ajax({
        url: '/Home/GetFurnaceData',
        type: 'GET',
        data: { prodDate: formattedDate },
        success: function (res) {

            if (res.MESSAGE) {
                alert(res.MESSAGE);
                return;
            }

            $("#CBF_ActOnDate").val(res.ACTUAL_C);
            $("#CBF_ReportOnDate").val(res.REPORTED_C);
            $("#CBF_Balance").val(res.BALANCE_C);

            $("#CBF_ActToDate").val(res.ACTUAL_C_TD);
            $("#CBF_ReportToDate").val(res.REPORTED_C_TD);
        }
    });
}
</script>
