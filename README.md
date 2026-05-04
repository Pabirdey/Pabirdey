let chartInstance = null;

$(document).ready(function () {
    loadFinesData();
});
function loadFinesData() {

    $.get('/RmbbPile/GetFinesData', function (res) {
        renderTable(res);
    });
}
function loadFinesData() {

    $.get('/RmbbPile/GetFinesData', function (res) {
        renderTable(res);
    });
}
function renderTable(data) {

    let html = '';

    data.forEach(item => {

        html += `
        <tr>
            <td>${item.ELEMENT}</td>

            <td class="chart-cell" data-type="RETURN_FINES" data-element="${item.ELEMENT}">
                ${item.RETURN_FINES}
            </td>

            <td class="chart-cell" data-type="WET_FINES" data-element="${item.ELEMENT}">
                ${item.WET_FINES}
            </td>

            <td class="chart-cell" data-type="DRY_FINES" data-element="${item.ELEMENT}">
                ${item.DRY_FINES}
            </td>

            <td class="chart-cell" data-type="DRY_FINES_500TPH" data-element="${item.ELEMENT}">
                ${item.DRY_FINES_500TPH}
            </td>
        </tr>`;
    });

    $("#finesTable tbody").html(html);
}

$(document).on("click", ".chart-cell", function () {

    let type = $(this).data("type");
    let element = $(this).data("element");

    loadTrend(type, element);
});
function loadTrend(type, element) {

    $.get('/RmbbPile/GetFinesTrend',
        { type: type, element: element },
        function (res) {

            $("#modalTitle").text(type + " - " + element);

            let modal = new bootstrap.Modal(document.getElementById('trendModal'));
            modal.show();

            setTimeout(() => {
                drawChart(res, element);
            }, 300);
        });
}
function drawChart(data, element) {

    if (chartInstance) {
        chartInstance.dispose();
    }

    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({
        tooltip: { trigger: 'axis' },

        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },

        yAxis: {
            type: 'value'
        },

        series: [{
            name: element,
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE)
        }]
    });
}
