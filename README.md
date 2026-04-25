function getValue(val) {
    if (val === null || val === undefined || val === "" || val === "null") {
        return '-';
    }
    return val;
}

function renderTable(data) {

    var html = '';

    if (!data || data.length === 0) {
        html = "<tr><td colspan='5'>No data found</td></tr>";
    }
    else {
        $.each(data, function (i, item) {
            html += '<tr>';

            html += '<td>' + getValue(item.ELEMENT) + '</td>';
            html += '<td>' + getValue(item.RETURN_FINES) + '</td>';
            html += '<td>' + getValue(item.WET_FINES) + '</td>';
            html += '<td>' + getValue(item.DRY_FINES) + '</td>';
            html += '<td>' + getValue(item.DRY_FINES_500TPH) + '</td>';

            html += '</tr>';
        });
    }

    $('#finesTable tbody').html(html);
}
