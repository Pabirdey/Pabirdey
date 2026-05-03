$(document).on("click", ".chart-cell", function () {

    let type = $(this).data("type");
    let value = $(this).text().trim();

    loadTrend(type, value);
});
