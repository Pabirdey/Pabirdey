function Get_Fugitive_Violin_Chart(pOvenNo, pDate, pBatteryNo, pPlantName) {
    debugger;

    // Show the modal and update title
    $('#FugitiveModal').modal('show'); // Use .modal('show') for Bootstrap modal
    $('.modal-title').text("Oven No " + pOvenNo);

    // Clear the existing chart
    Plotly.purge('modalPushCurrentChart1');

    // Make AJAX call to controller
    $.ajax({
        url: '@Url.Action("Get_Fugitive_Violin_Chart", "YourControllerName")', // Ensure correct controller
        type: 'POST',
        data: {
            pTimestamp: pDate,
            pOvenNo: pOvenNo,
            pBatteryNo: pBatteryNo,
            pPlantName: pPlantName
        },
        success: function (jData) {
            if (!jData || jData.length === 0) {
                alert("No data found for selected input.");
                return;
            }

            var values = jData.map(item => item.PUSH_FORCE);
            var labels = jData.map(item => item.DATETIME);

            var dataPlot = [{
                type: 'violin',
                y: values,
                x: labels,
                box: { visible: true },
                line: { color: 'blue' },
                meanline: { visible: true },
                points: 'all',
                jitter: 0.5,
                scalemode: 'count',
                name: 'Push Force'
            }];

            var layout = {
                title: "Fugitive Violin Chart",
                yaxis: { zeroline: false, title: "Push Force" },
                xaxis: { title: "Date/Time", type: 'category' }, // if too many dates, consider hiding ticks
                margin: { t: 50 }
            };

            Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
        },
        error: function (xhr, status, error) {
            console.error("Error loading violin chart:", error);
            alert("Error: " + xhr.responseText);
        }
    });
}