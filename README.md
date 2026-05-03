function loadCokeData() {

    var shift = $("#ddlshift").val();

    $.ajax({
        url: '/Furnace_High_line/Get_Coke_Unloading',
        type: 'GET',
        data: {
            date: lsSelectedFDate,
            shift: shift
        },
        success: function (res) {

            let tbody = $("#tblBody");
            tbody.empty();

            if (res.success && res.data.length > 0) {

                // ✅ Show DB data
                res.data.forEach(function (item) {
                    tbody.append(createRow(item));
                });

            } else {

                // ✅ No data → create 8 blank rows
                for (let i = 0; i < 8; i++) {
                    tbody.append(createRow());
                }
            }

            // ✅ Copy header date & shift
            copyDateShiftToRows();
        },
        error: function () {
            alert("Error loading data");
        }
    });
}
