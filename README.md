function SaveCastHouseData() {
    debugger;

    // 1. Get all rows from all Cast House tables
    var rows = document.querySelectorAll(".cast-table tbody tr");
    var CastHouseMap = {};

    rows.forEach(function (row) {
        var inputs = row.querySelectorAll("input, select");
        var castNo = "";
        var rowData = {};

        inputs.forEach(function (input) {
            let val = input.value.trim();
            rowData[input.name] = val === "" ? null : val;
            if (input.name === "cast_no") {
                castNo = val;
            }
        });

        // Skip rows without a cast number
        if (!castNo) return;

        // Merge into one object per cast_no
        if (!CastHouseMap[castNo]) {
            CastHouseMap[castNo] = rowData;
        } else {
            Object.assign(CastHouseMap[castNo], rowData);
        }
    });

    // 2. Convert map to array
    var CastHouse = Object.values(CastHouseMap);

    // 3. Get selected date & furnace
    var selectedDate = document.getElementById("tbFDatePick").value.trim();
    var selectedFurnace = document.getElementById("lstFur").value.trim();

    console.log(CastHouse);

    // 4. Send data via AJAX
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
                    text: 'Data Saved successfully!',
                    showConfirmButton: true
                });
            } else {
                Swal.fire({
                    icon: 'error',
                    title: 'Failed!',
                    text: response.message || 'Data could not be saved. Please try again.'
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
function SaveCastHouseData() {
    debugger;

    // 1. Get all rows from all Cast House tables
    var rows = document.querySelectorAll(".cast-table tbody tr");
    var CastHouseMap = {};

    rows.forEach(function (row) {
        var inputs = row.querySelectorAll("input, select");
        var castNo = "";
        var rowData = {};

        inputs.forEach(function (input) {
            let val = input.value.trim();
            rowData[input.name] = val === "" ? null : val;
            if (input.name === "cast_no") {
                castNo = val;
            }
        });

        // Skip rows without a cast number
        if (!castNo) return;

        // Merge into one object per cast_no
        if (!CastHouseMap[castNo]) {
            CastHouseMap[castNo] = rowData;
        } else {
            Object.assign(CastHouseMap[castNo], rowData);
        }
    });

    // 2. Convert map to array
    var CastHouse = Object.values(CastHouseMap);

    // 3. Get selected date & furnace
    var selectedDate = document.getElementById("tbFDatePick").value.trim();
    var selectedFurnace = document.getElementById("lstFur").value.trim();

    console.log(CastHouse);

    // 4. Send data via AJAX
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
                    text: 'Data Saved successfully!',
                    showConfirmButton: true
                });
            } else {
                Swal.fire({
                    icon: 'error',
                    title: 'Failed!',
                    text: response.message || 'Data could not be saved. Please try again.'
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
