
function drawChart(data, element, type) {
    if (chartInstance != null) {
        chartInstance.dispose();
    }
    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({
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
            name: type
        },
        series: [{
            name: element + " (" + type + ")",
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE),
            lineStyle: { width: 3 }
        }]
    });
}
