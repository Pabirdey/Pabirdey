function Display_Bin_Position() {
    debugger;

    var shift = $("#ddlshift").val();

    $.ajax({
        url: '/Furnace_High_line/Get_Bin_Position',
        type: 'GET',
        data: { date: lsSelectedFDate, shift: shift },

        success: function (res) {
            console.log(res);

            if (res.success) {
                $(".cell").val("");

                res.data.forEach(function (item) {
                    var input = document.querySelector('.cell[data-id="' + item.CellId + '"]');
                    if (input) {
                        input.value = item.Value;
                    }
                });
            } else {
                alert(res.message);
            }
        },

        error: function () {
            alert("Error Loading Data");
        }
    });
}
