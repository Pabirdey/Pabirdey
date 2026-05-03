$(document).on("click", ".chart-cell", function () {

    let type = $(this).data("type");

    loadTrend(type);
});
function loadTrend(type) {

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesTrend',
        type: 'GET',
        data: { type: type },
        success: function (res) {

            $("#trendModal").modal("show");

            drawChart(res);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}
function drawChart(data) {

    if (chartInstance != null) {
        chartInstance.dispose();
    }

    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({
        tooltip: { trigger: 'axis' },

        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },

        yAxis: {
            type: 'value'
        },

        series: [{
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE),
            lineStyle: { width: 3 }
        }]
    });
}
</script>
