function Get_CP_Fugitivity_Voilin_Chart(pOvenNo, pDate) {
    debugger;
    var modal = $('#FugitiveModal');
    modal.modal('show');
    modal.find('.modal-title').text("Oven No " + pOvenNo);

    var pBatteryNo = $('#battery_no').val();
    var pPlantName = $('#Area').val(); // FIX: was 'Area' (undefined), now it's correct

    Plotly.purge('modalPushCurrentChart1');

    $.post('@Url.Action("Get_cp_fugitive_Voilin_Chart")', {
        pTimestamp: pDate,
        pOvenNo: pOvenNo,
        pBatteryNo: pBatteryNo,
        pPlantName: pPlantName // FIX: Use pPlantName variable
    })
    .done(function (data) {
        if (typeof data === "string") {
            try {
                data = JSON.parse(data);
            } catch (e) {
                alert("Data parse error: " + e.message);
                console.error(data);
                return;
            }
        }

        let pushForces = data.map(row => parseFloat(row.PUSH_FORCE)).filter(v => !isNaN(v));

        let trace = {
            type: 'violin',
            y: pushForces,
            box: { visible: true },
            line: { color: 'orange' },
            meanline: { visible: true },
            name: 'Fugitive',
            points: 'all',
            jitter: 0.5,
            scalemode: 'count'
        };

        let layout = {
            title: 'Violin Chart - Fugitive',
            yaxis: {
                title: 'Fugitive',
                zeroline: true,
                zerolinewidth: 2,
                zerolinecolor: 'gray',
                range: [Math.min(...pushForces) - 5, Math.max(...pushForces) + 5] // Handles negative values
            },
            margin: { t: 40, l: 60, r: 30, b: 50 }
        };

        Plotly.newPlot('modalPushCurrentChart1', [trace], layout);
    })
    .fail(function (xhr, status, error) {
        alert("AJAX Error: " + error);
        console.error(xhr.responseText);
    });
}