function loadTrend(type) {

    $.ajax({
        url: '/Ore_Beneficiation/GetFinesTrend',
        type: 'GET',
        data: { type: type },
        success: function (res) {

            const modalEl = document.getElementById('trendModal');

            const modal = new bootstrap.Modal(modalEl);

            modal.show();

            // 🔥 IMPORTANT: wait until modal is fully visible
            setTimeout(function () {
                drawChart(res);
            }, 300);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}
