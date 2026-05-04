function loadTrend(type, element) {

    $.ajax({
        url: '/RmbbPile/GetFinesTrend',
        type: 'GET',
        data: { type: type, element: element },   // ✅ pass element

        success: function (res) {

            const modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();

            // Optional title
            $("#modalTitle").text(type + " - " + element);

            setTimeout(function () {
                drawChart(res);
            }, 300);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}
