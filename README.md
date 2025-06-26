$.post('@Url.Action("Get_Voilin_Chart")', {
    pTimestamp: pDate,
    pOvenNo: pOvenNo,
    pBatteryNo: pBatteryNo,                
    pPlantName: Area
})
.done(function (data) {
    // ✅ Check if data is a string; if so, parse it
    if (typeof data === "string") {
        try {
            data = JSON.parse(data);
        } catch (e) {
            alert("Data parse error: " + e.message);
            console.error(data);
            return;
        }
    }

    // ✅ Now you can safely call .map()
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
    alert("AJAX Error: " + error);
    console.error(xhr.responseText);
});