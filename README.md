function createRow(item = {}) {

    return `
    <tr>
        <td>
            <input type="text" class="form-control row-date" style="width:100px;" 
            value="${formatDate(item.TIMESTAMP)}" readonly>
        </td>

        <td>
            <select class="form-control row-shift">
                <option ${item.SHIFT == 'A' ? 'selected' : ''}>A</option>
                <option ${item.SHIFT == 'B' ? 'selected' : ''}>B</option>
                <option ${item.SHIFT == 'C' ? 'selected' : ''}>C</option>
            </select>
        </td>

        <td>
            <select class="form-control bunker">
                <option value="">---Pls. Select---</option>
                <option ${item.BUNKER=='WESTERN'?'selected':''}>WESTERN</option>
                <option ${item.BUNKER=='MIDDLE'?'selected':''}>MIDDLE</option>
                <option ${item.BUNKER=='EASTERN'?'selected':''}>EASTERN</option>
                <option ${item.BUNKER=='H/S NC'?'selected':''}>H/S NC</option>
                <option ${item.BUNKER=='NC BF KO'?'selected':''}>NC BF KO</option>
            </select>
        </td>

        <td><input class="form-control val" value="${item.C || ''}"></td>
        <td><input class="form-control val" value="${item.E || ''}"></td>
        <td><input class="form-control val" value="${item.F || ''}"></td>

        <td><input class="form-control total" value="${item.TOTAL || ''}" readonly></td>

        <td><input class="form-control position" value="${item.BUNKER_P || ''}"></td>
        <td><input class="form-control balance" value="${item.BALANCE || ''}"></td>
    </tr>`;
}

$(document).ready(function () {

    $.ajax({
        url: '/Home/GetData',
        type: 'GET',
        success: function (data) {

            let tbody = $("#tblBody");
            tbody.empty();

            if (data.length > 0) {

                data.forEach(function (item) {
                    tbody.append(createRow(item)); // ✅ merged
                });

            } else {

                // if no data → create blank rows
                for (let i = 0; i < 8; i++) {
                    tbody.append(createRow());
                }
            }
        }
    });

});
