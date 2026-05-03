function renderTable(data) {

    let html = '';

    if (!data || data.length === 0) {
        html = "<tr><td colspan='5'>No Data Found</td></tr>";
    }
    else {
        data.forEach(item => {

            html += `
            <tr>
                <td class="chart-cell" data-type="ELEMENT">${item.ELEMENT}</td>
                <td class="chart-cell" data-type="RETURN_FINES">${item.RETURN_FINES}</td>
                <td class="chart-cell" data-type="WET_FINES">${item.WET_FINES}</td>
                <td class="chart-cell" data-type="DRY_FINES">${item.DRY_FINES}</td>
                <td class="chart-cell" data-type="DRY_FINES_500TPH">${item.DRY_FINES_500TPH}</td>
            </tr>`;
        });
    }

    $("#finesTable tbody").html(html);
}
