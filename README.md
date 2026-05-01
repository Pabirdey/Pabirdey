function Save_Bin_Position() {

    var dataList = [];

    $(".cell").each(function () {
        dataList.push({
            CellId: $(this).data("id"),
            Value: $(this).val(),
            Date: lsSelectedFDate,
            Shift: $("#ddlshift").val()
        });
    });

    $.ajax({
        url: '/Furnace_High_line/Save_Furnace_High_Line',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify({ list: dataList }),

        success: function (res) {
            if (res.success) {
                alert(res.message);   // ✅ SAVE MESSAGE DISPLAY
            } else {
                alert("Error: " + res.message);
            }
        },

        error: function () {
            alert("Save failed!");
        }
    });
}
