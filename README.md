function DisplayHotMetalAnalysis() {

    $.ajax({
        url: '/Granshot/GetHotMetalAnalysis',
        type: 'GET',
        data: {
            pdate: lsSelectedFDate,
            pshift: $("#ddlshift").val(),
            parea: 'GRANSHOT'
        },
        success: function (data) {

            $("#tblHotMetalBody").empty();

            if (data.length > 0) {

                for (var i = 0; i < data.length; i++) {

                    var row = `<tr>
                        <td><input type="text" class="table-input" value="${data[i].CASTNO || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].TP || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].HOTMETAL_TIME || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].C || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].SI || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].S || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].MN || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].TI || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].P || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].CR || ''}"></td>
                        <td><input type="text" class="table-input" value="${data[i].BORON || ''}"></td>
                    </tr>`;

                    $("#tblHotMetalBody").append(row);
                }
            }
            else {

                // Show 8 blank rows if no data found
                for (var i = 0; i < 8; i++) {

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
                    </tr>`;

                    $("#tblHotMetalBody").append(row);
                }
            }
        }
    });
}
