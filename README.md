let chartInstance = null;

$(document).ready(function () {
    loadFinesData();
});

// CLICK CELL
$(document).on("click", ".chart-cell", function () {
    let type = $(this).data("type");
    loadTrend(type);
