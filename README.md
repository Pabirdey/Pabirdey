$(document).on("click", ".chart-cell", function () {
    let type = $(this).data("type");
    let element = $(this).data("element");
    loadTrend(type, element);
});
