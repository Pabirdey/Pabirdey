function loadTrend(type, value) {

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesTrend',
        type: 'GET',
        data: {
            type: type,
            value: value
        },
        success: function (res) {

            $("#trendModal").modal("show");

            drawChart(res);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}
