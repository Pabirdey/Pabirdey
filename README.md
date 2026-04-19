function SaveBFData() {

    debugger;

    var date = $("#txtDate").val();

    if (!date) {
        alert("Please select date");
        return;
    }

    var furnaces = ["C", "E", "F"];
    var modelList = [];

    furnaces.forEach(function (f) {

        var model = {
            FURNACE: f,

            // 🔥 DATE ADDED HERE
            DATE_TIME: date,

            ACT_ONDT: Number($("#" + f + "_ActOnDate").val()) || 0,
            REPORT_ONDT: Number($("#" + f + "_ReportOnDate").val()) || 0,
            BALANCE: Number($("#" + f + "_Balance").val()) || 0
        };

        modelList.push(model);
    });

    $.ajax({
        url: '/HML/SaveBFProdData',
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
