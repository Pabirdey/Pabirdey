function GenerateNewCast() {

    $.ajax({
        url: '/Granshot/GetNextCastNo',
        type: 'GET',
        success: function (castNo) {

            var isRowFound = false;

            $("#tblBody tr").each(function () {

                var castNoTextbox = $(this).find("td:eq(0) input");

                if ($.trim(castNoTextbox.val()) === "") {

                    // Fill Cast No in first empty row
                    castNoTextbox.val(castNo);

                    // Optional: focus next column
                    $(this).find("td:eq(1) input").focus();

                    isRowFound = true;
                    return false; // break loop
                }
            });

            // If no empty row exists then create a new row
            if (!isRowFound) {

                var newRow = `
                <tr>
                    <td><input type="text" class="table-input" value="${castNo}"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>

                    <td>
                        <select class="table-input arrivedFrom">
                            <option value=""></option>
                            <option value="C">C</option>
                            <option value="E">E</option>
                            <option value="F">F</option>
                            <option value="G">G</option>
                            <option value="H">H</option>
                            <option value="I">I</option>
                        </select>
                    </td>

                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><input type="text" class="table-input"></td>
                    <td><button type="button" class="btnDelete">Delete</button></td>
                </tr>`;

                $("#tblBody").append(newRow);
            }
        },
        error: function () {
            alert("Unable to generate Cast No.");
        }
    });
}
