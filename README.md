function BindTable(data) {

    $("#tblBody").empty();

    var totalRows = 15;
    var dataCount = data.length;

    // Bind existing data
    if (dataCount > 0) {

        $.each(data, function (i, item) {

            var row = `<tr>
                <td><input type="text" class="table-input" value="${item.CAST_NO || ''}"></td>
                <td><input type="text" class="table-input" value="${item.CAST_ST_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.CAST_END_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.TRP_NO || ''}"></td>
                <td><input type="text" class="table-input" value="${item.LADLE_FLST_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.LADLE_FLEND_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.ARRIVED_FROM || ''}"></td>
                <td><input type="text" class="table-input" value="${item.GROSS_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.TARE_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.NET_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.POURING_RATE || ''}"></td>
                <td><input type="text" class="table-input" value="${item.HMT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.REASON_POURING || ''}"></td>
                <td><input type="text" class="table-input" value="${item.SEQ_NO || ''}"></td>
                <td><button type="button">Delete</button></td>
            </tr>`;

            $("#tblBody").append(row);
        });

        // Add blank rows up to 15
        for (var i = dataCount; i < totalRows; i++) {
            AddBlankRow();
        }
    }
    else {

        // No data, create 15 blank rows
        for (var i = 0; i < totalRows; i++) {
            AddBlankRow();
        }
    }
}

function AddBlankRow() {

    var row = `<tr>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><input type="text" class="table-input"></td>
        <td><button type="button">Delete</button></td>
    </tr>`;

    $("#tblBody").append(row);
}
