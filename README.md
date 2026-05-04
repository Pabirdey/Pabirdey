function drawChart(data, element, type) {

    if (chartInstance != null) {
        chartInstance.dispose();
    }

    chartInstance = echarts.init(document.getElementById("trendChart"));

    let dates = data.map(x => x.DATE);
    let values = data.map(x => x.VALUE);

    chartInstance.setOption({

        // ✅ Title
        title: {
            text: element + " - " + type.replaceAll("_", " "),
            left: 'center',
            textStyle: {
                fontSize: 16,
                fontWeight: 'bold'
            }
        },

        // ✅ Tooltip (hover effect)
        tooltip: {
            trigger: 'axis',
            backgroundColor: '#333',
            borderRadius: 5,
            textStyle: { color: '#fff' }
        },

        // ✅ Zoom (very useful 🔥)
        dataZoom: [
            { type: 'inside' },
            { type: 'slider' }
        ],

        // ✅ Grid spacing
        grid: {
            left: '8%',
            right: '5%',
            bottom: '12%'
        },

        // ✅ X Axis
        xAxis: {
            type: 'category',
            data: dates,
            boundaryGap: false,
            axisLine: { lineStyle: { color: '#888' } }
        },

        // ✅ Y Axis
        yAxis: {
            type: 'value',
            name: type.replaceAll("_", " "),
            axisLine: { show: true },
            splitLine: {
                lineStyle: {
                    type: 'dashed',
                    color: '#ddd'
                }
            }
        },

        // ✅ Series (Main Beauty Part 🔥)
        series: [{
            name: element,
            type: 'line',
            smooth: true,

            data: values,

            // 🔥 Line Style
            lineStyle: {
                width: 3,
                color: '#5470C6'
            },

            // 🔥 Point Style
            symbol: 'circle',
            symbolSize: 6,

            itemStyle: {
                color: '#5470C6'
            },

            // 🔥 Area Gradient
            areaStyle: {
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                    { offset: 0, color: 'rgba(84,112,198,0.5)' },
                    { offset: 1, color: 'rgba(84,112,198,0.05)' }
                ])
            },

            // 🔥 Show max & min points
            markPoint: {
                data: [
                    { type: 'max', name: 'Max' },
                    { type: 'min', name: 'Min' }
                ]
            }
        }]
    });
}
