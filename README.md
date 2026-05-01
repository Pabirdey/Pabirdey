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

                    var id = item.CellId ? item.CellId.trim() : "";

                    console.log("Matching ID:", id);

                    var inputs = document.querySelectorAll('.cell[data-id="' + id + '"]');

                    if (inputs.length > 0) {
                        inputs.forEach(function (input) {
                            input.value = item.Value;
                        });
                    } else {
                        console.warn("No matching element for:", id);
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
