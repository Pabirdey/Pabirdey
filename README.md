$.ajax({
    url: '/HML/GetProductionSummary',
    type: 'GET',
    data: { txtdt: $("#txtDate").val() },
    success: function (data) {

        $("#txtLD1C").val(data.LD1C);
        $("#txtLD2C").val(data.LD2C);
        $("#txtLD3C").val(data.LD3C);

        $("#txtLD1E").val(data.LD1E);
        $("#txtLD2E").val(data.LD2E);

        $("#txtLD1TOT").val(data.LD1TOT);
        $("#txtLD2TOT").val(data.LD2TOT);
        $("#txtLD3TOT").val(data.LD3TOT);
    }
});
