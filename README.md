<script>
function loadData() {

    var date = $("#txtDate").val();
    var formattedDate = date.replace("T", " ") + ":00";

    $.ajax({
        url: '/Home/GetFurnaceData',
        type: 'GET',
        data: { prodDate: formattedDate },
        success: function (data) {

            // if no data
            if (data.message) {
                alert(data.message);
                return;
            }

            data.forEach(function (item) {

                if (item.FURNACE === "C") {
                    $("#CBF_ActOnDate").val(item.ACT_ONDT);
                    $("#CBF_ActToDate").val(item.ACT_TODT);
                    $("#CBF_ReportOnDate").val(item.REPORT_ONDT);
                    $("#CBF_ReportToDate").val(item.REPORT_TODT);
                    $("#CBF_Balance").val(item.BALANCE);
                }

                if (item.FURNACE === "E") {
                    $("#EBF_ActOnDate").val(item.ACT_ONDT);
                    $("#EBF_ActToDate").val(item.ACT_TODT);
                    $("#EBF_ReportOnDate").val(item.REPORT_ONDT);
                    $("#EBF_ReportToDate").val(item.REPORT_TODT);
                    $("#EBF_Balance").val(item.BALANCE);
                }

                if (item.FURNACE === "F") {
                    $("#FBF_ActOnDate").val(item.ACT_ONDT);
                    $("#FBF_ActToDate").val(item.ACT_TODT);
                    $("#FBF_ReportOnDate").val(item.REPORT_ONDT);
                    $("#FBF_ReportToDate").val(item.REPORT_TODT);
                    $("#FBF_Balance").val(item.BALANCE);
                }

            });
        }
    });
}
</script>
