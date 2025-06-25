$(document).on('click', '.oven-cell', function () {
    const ovenNo = $(this).data('oven');
    const date = $(this).data('date');
    const batteryNo = $(this).data('battery');

    // Show modal for violin chart
    $('#FugitiveModal').modal('show');
    $('.modal-title').text("Oven No " + ovenNo);

    // Clear old chart
    Plotly.purge('modalPushCurrentChart1');

    // AJAX to fetch data
    $.post('@Url.Action("GetFugitiveViolinChart")', {
        pOvenNo: ovenNo,
        pDate: date,
        pBatteryNo: batteryNo
    }, function (response) {
        // Plotly violin chart
        Plotly.newPlot('modalPushCurrentChart1', response.chartData, response.layout);
    });
});