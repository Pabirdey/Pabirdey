function Get_Fugitive_Violin_Chart(pOvenNo, pDate) {
    debugger;

    // Set modal title
    var modal = $('#FugitiveModal');
    modal.find('.modal-title').text("Oven No " + pOvenNo);

    // Clear any existing chart in the DOM element
    Plotly.purge('modalPushCurrentChart1');

    var pBatteryNo = $('#battery_no').val();

    $.post('@Url.Action("Get_Fugitive_Violin_Chart")', {
        'pTimestamp': pDate,
        'pOvenNo': pOvenNo,
        'pBatteryNo': pBatteryNo,
        'pPlantName': Area
    }, function (data) {
        var jData = JSON.parse(data);

        // Prepare chart data
        var values = jData.map(item => item.Value);
        var labels = jData.map(item => item.Label);

        var dataPlot = [{
            type: 'violin',
            y: values,
            x: labels,
            box: {
                visible: true
            },
            line: {
                color: 'blue'
            },
            meanline: {
                visible: true
            }
        }];

        var layout = {
            title: "Fugitive Violin Chart",
            yaxis: {
                zeroline: false
            }
        };

        Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
    });
}