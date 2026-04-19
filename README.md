function saveCBFData() {

    var furnaces = ["C", "E", "F"];   // 👉 add more if needed

    var modelList = [];

    furnaces.forEach(function (f) {

        var model = {
            FURNACE_C: f,

            ACT_ONDT: Number($("#" + f + "_ActOnDate").val()) || 0,
            ACT_TODT: Number($("#" + f + "_ActToDate").val()) || 0,

            REPORT_ONDT: Number($("#" + f + "_ReportOnDate").val()) || 0,
            REPORT_TODT: Number($("#" + f + "_ReportToDate").val()) || 0,

            BALANCE: Number($("#" + f + "_Balance").val()) || 0
        };

        modelList.push(model);
    });

    $.ajax({
        url: '/Home/SaveCBFBulk',   // 👈 bulk API
        type: 'POST',
        data: JSON.stringify(modelList),
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
