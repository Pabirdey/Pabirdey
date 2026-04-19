function saveCBFData() {

    var model = {
        FURNACE_C: $("#CBF_Furnace").val(),

        ACT_ONDT: Number($("#CBF_ActOnDate").val()) || 0,
        ACT_TODT: Number($("#CBF_ActToDate").val()) || 0,

        REPORT_ONDT: Number($("#CBF_ReportOnDate").val()) || 0,
        REPORT_TODT: Number($("#CBF_ReportToDate").val()) || 0,

        BALANCE: Number($("#CBF_Balance").val()) || 0
    };

    $.ajax({
        url: '/Home/SaveCBFData',
        type: 'POST',
        data: JSON.stringify(model),
        contentType: 'application/json; charset=utf-8',
        dataType: 'json',

        success: function (res) {
            if (res.success) {
                alert("Saved Successfully");
            } else {
                alert("Error: " + res.message);
            }
        },

        error: function () {
            alert("Server error");
        }
    });
}
