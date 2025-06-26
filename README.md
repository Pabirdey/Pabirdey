function Get_CP_Fugitivity_Voilin_Chart(pOvenNo, pDate) {
    var modal = $('#FugitiveModal');
    modal.modal('show'); // Ensure modal is shown
    modal.find('.modal-title').text("Oven No " + pOvenNo);

    var pBatteryNo = $('#battery_no').val();
    var pSCP = $('#hf_PC_SCP').val();
    var Area = $('#hfArea').val(); // Ensure Area is provided

    Plotly.purge('modalPushCurrentChart1'); // Clear existing chart

    $.post('@Url.Action("Get_CP_Fugitivity_Voilin_Chart")', {
        pTimestamp: pDate,
        pOvenNo: pOvenNo,
        pBatteryNo: pBatteryNo,
        pSCP: pSCP,
        pPlantName: Area
    }, function (data) {
        let parsed = JSON.parse(data);
        let pushForces = parsed.map(row => parseFloat(row.PUSH_FORCE));

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
    });
}