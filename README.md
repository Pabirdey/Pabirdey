function SaveCastHouseData() {
    debugger;
    var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr,#Mudgun_Details tbody tr,#Other_Details tr");
    var CastHouseMap = {};
    rows.forEach(function (row) {
        var inputs = row.querySelectorAll("input, select");
        var castNo = "";
        var rowData = {};
        inputs.forEach(function (input) {
            let val = input.value.trim();
            rowData[input.name] = val === "" ? null : val;
            if (input.name === "CAST_NO") {
                castNo = val;
            }
        });
        if (!CastHouseMap[castNo]) {
            CastHouseMap[castNo] = rowData;
        } else {
            Object.assign(CastHouseMap[castNo], rowData);
        }
    });
    var CastHouse = Object.values(CastHouseMap);
    var selectedDate = document.getElementById("tbFDatePick").value.trim();
    var selectedFurnace = document.getElementById("lstFur").value.trim();
    console.log(CastHouse);
    console.log(selectedDate);
    console.log(selectedFurnace);
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
                    text: 'Data Saved Successfully!',
                    showConfirmButton: true
                });
            } else {
                Swal.fire({
                    icon: 'error',
                    title: 'Failed!',
                    text: response.message || 'Data Could not be Saved.Please try again....'
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
