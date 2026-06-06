function BindTable(data) {

    $("#tblBody").empty();

    // Data found
    if (data.length > 0) {

        $.each(data, function (i, item) {

            var row = `<tr>
                <td><input type="text" class="form-control castno" value="${item.CAST_NO || ''}"></td>
                <td><input type="text" class="form-control" value="${item.CAST_ST_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.CAST_END_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.TRP_NO || ''}"></td>
                <td><input type="text" class="form-control" value="${item.LADLE_FLST_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.LADLE_FLEND_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.ARRIVED_FROM || ''}"></td>
                <td><input type="text" class="form-control" value="${item.GROSS_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.TARE_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.NET_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.POURING_RATE || ''}"></td>
                <td><input type="text" class="form-control" value="${item.HMT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.REASON_POURING || ''}"></td>
                <td><input type="text" class="form-control" value="${item.SEQ_NO || ''}"></td>
                <td><button type="button">Delete</button></td>
            </tr>`;

            $("#tblBody").append(row);
        });
    }
    else {

        // No data found - show 8 blank rows
        for (var i = 1; i <= 8; i++) {

            var row = `<tr>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><button type="button">Delete</button></td>
            </tr>`;

            $("#tblBody").append(row);
        }
    }
}
