function SaveCastHouseData() {

    var rows = document.querySelectorAll(
        "#TAP_Hot_Metal_Details tbody tr," +
        "#Driling_Slag_Details tbody tr," +
        "#Mudgun_Details tbody tr," +
        "#Other_Details tbody tr"
    );

    var CastHouseMap = {};

    rows.forEach(function (row) {

        // 🔹 GET CAST NO FROM FIRST TD (freeze column)
        var castCell = row.querySelector("td.freeze-col, td[data-castno]");
        if (!castCell) return;

        var castNo = castCell.innerText.trim();
        if (!castNo) return;

        if (!CastHouseMap[castNo]) {
            CastHouseMap[castNo] = { CAST_NO: castNo };
        }

        var inputs = row.querySelectorAll("input, select");

        inputs.forEach(function (input) {

            if (!input.name) return; // 🔥 skip unnamed fields

            let val = input.value ? input.value.trim() : null;
            CastHouseMap[castNo][input.name] = val === "" ? null : val;
        });
    });

    var CastHouse = Object.values(CastHouseMap);

    var selectedDate = document.getElementById("tbFDatePick").value.trim();
    var selectedFurnace = document.getElementById("lstFur").value.trim();

    console.log("FINAL DATA →", CastHouse);

    $.ajax({
        url: '/CastHouse/SaveCastHouseData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify({
            data: CastHouse,
            Fdate: selectedDate,
            Fur: selectedFurnace
        }),
        success: function (response) {
            if (response.success) {
                Swal.fire({
                    icon: 'success',
                    text: 'Data Saved Successfully!'
                });
            } else {
                Swal.fire({
                    icon: 'error',
                    title: 'Failed!',
                    text: response.message || 'Data could not be saved'
                });
            }
        },
        error: function () {
            Swal.fire({
                icon: 'error',
                title: 'Error!',
                text: 'Something went wrong while saving.'
            });
        }
    });
}
