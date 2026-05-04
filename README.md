function renderTable(data) {

    let html = '';

    if (!data || data.length === 0) {
        html = "<tr><td colspan='5'>No Data Found</td></tr>";
    }
    else {
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
    }

    $("#finesTable tbody").html(html);
}
