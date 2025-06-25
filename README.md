function Get_Fugitive_Violin_Chart(pOvenNo, pDate, pBatteryNo, pPlantName) {
    $('#FugitiveModal').show();
    $('.modal-title').text("Oven No " + pOvenNo);
    Plotly.purge('modalPushCurrentChart1');

    $.post('@Url.Action("Get_Fugitive_Violin_Chart")', {
        'pTimestamp': pDate,
        'pOvenNo': pOvenNo,
        'pBatteryNo': pBatteryNo,
        'pPlantName': pPlantName
    }, function (jData) {
        if (!jData || jData.length === 0 || jData.success === false) {
            alert("No data or error: " + (jData.message || "Unknown error"));
            return;
        }

        var values = jData.map(item => item.PUSH_FORCE);
        var labels = jData.map(item => item.DATETIME);

        var dataPlot = [{
            type: 'violin',
            y: values,
            x: labels,
            box: { visible: true },
            line: { color: 'blue' },
            meanline: { visible: true }
        }];

        var layout = {
            title: "Fugitive Violin Chart",
            yaxis: { zeroline: false, title: "Push Force" },
            xaxis: { title: "Date" }
        };

        Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
    }).fail(function (xhr, status, error) {
        alert("Error: " + xhr.responseText);
    });
}