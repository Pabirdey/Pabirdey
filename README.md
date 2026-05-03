function drawChart(data) {

    echarts.init(document.getElementById("trendChart"))
        .setOption({
            xAxis: {
                type: 'category',
                data: data.map(d => d.DATE)
            },
            yAxis: {
                type: 'value'
            },
            series: [{
                type: 'line',
                data: data.map(d => d.VALUE)
            }]
        });
}
