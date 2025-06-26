$.post('@Url.Action("Get_Voilin_Chart")', {
    pTimestamp: pDate,
    pOvenNo: pOvenNo,
    pBatteryNo: pBatteryNo,                
    pPlantName: Area
})
.done(function (data) {
    if (data.error) {
        alert("Server error: " + data.error); // Show error from server
        return;
    }

    let pushForces = data.map(row => parseFloat(row.PUSH_FORCE));
    let trace = {
        type: 'violin',
        y: pushForces,
        box: { visible: true },
        line: { color: 'blue' },
        meanline: { visible: true },
        name: 'Push Force',
    };
    let layout = {
        title: 'Violin Chart - Push Force',
        yaxis: { title: 'Push Force (kg)' }
    };
    Plotly.newPlot('modalPushCurrentChart1', [trace], layout);
})
.fail(function (xhr, status, error) {
    alert("AJAX Error: " + error); // show client-side error
    console.error(xhr.responseText);
});