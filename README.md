<td>
    <input type="text"
           class="table-input"
           value="${item.TLC_FINAL_DATE ? new Date(parseInt(item.TLC_FINAL_DATE.replace('/Date(', '').replace(')/', ''))).toLocaleDateString('en-GB') : ''}"
           readonly>
</td>

function formatDate(jsonDate) {
    if (!jsonDate) return '';

    var timestamp = parseInt(jsonDate.replace('/Date(', '').replace(')/', ''));
    var date = new Date(timestamp);

    return date.toLocaleDateString('en-GB');
}

<td>
    <input type="text"
           class="table-input"
           value="${formatDate(item.TLC_FINAL_DATE)}"
           readonly>
</td>
