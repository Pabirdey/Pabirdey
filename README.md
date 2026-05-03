let chartInstance = null;

$(document).on("click", ".clickable", function () {

    let element = $(this).data("element");   // AL2O3
    let type = $(this).data("type");         // Return Fines

    $("#trendModal").modal("show");

    $.ajax({
        url: '/YourController/Get30DaysData',
        type: 'GET',
        data: { element: element, type: type },
        success: function (res) {

            let labels = [];
            let values = [];

            res.forEach(x => {
                labels.push(x.DATE);
                values.push(x.VALUE);
            });

            drawChart(labels, values, element + " - " + type);
        }
    });
});
