function loadTrend(type) {

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesTrend',
        type: 'GET',
        data: { type: type },
        success: function (res) {

            // ✅ Bootstrap 5 correct modal open
            const modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();

            drawChart(res);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}
