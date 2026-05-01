function SaveBinPosition() {

    var list = [];
    var shift = $("#ddlshift").val();

    $(".cell").each(function () {
        list.push({
            CellId: $(this).data("id"),
            Value: $(this).val(),
            Date: lsSelectedFDate,
            Shift: shift
        });
    });

    console.log(list);

    $.ajax({
        url: '/Furnace_High_line/Save_Furnace_High_Line',
        type: 'POST',
        data: JSON.stringify({ list: list }),   // ✅ important fix
        contentType: 'application/json',

        success: function (res) {
            if (res.success) {
                alert(res.message);   // ✅ show controller message
            }
            else {
                alert(res.message);   // ✅ show error message
            }
        },

        error: function () {
            alert("Save failed!");
        }
    });
}
