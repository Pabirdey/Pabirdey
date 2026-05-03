
<script src="https://cdn.jsdelivr.net/npm/echarts@5.5.0/dist/echarts.min.js"></script>

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
