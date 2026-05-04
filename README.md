function drawChart(data, element, type) {

    if (chartInstance != null) {
        chartInstance.dispose();
    }

    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({

        // ✅ Show Title
        title: {
            text: element + " - " + type + " (30 Days Trend)",
            left: 'center'
        },

        tooltip: { trigger: 'axis' },

        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },

        yAxis: {
            type: 'value',
            name: type   // ✅ Y-axis label
        },

        series: [{
            name: element + " (" + type + ")",   // ✅ Legend name
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE),
            lineStyle: { width: 3 }
        }]
    });
}
function loadTrend(type, element) {

    $.ajax({
        url: '/RmbbPile/GetFinesTrend',
        type: 'GET',
        data: { type: type, element: element },

        success: function (res) {

            const modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();

            // ✅ Modal title also
            $("#modalTitle").text(element + " - " + type);

            setTimeout(function () {
                drawChart(res, element, type);   // ✅ pass both
            }, 300);
        }
    });
}
