function copyDateShiftToRows() {

    // Get header values
    var headerDate = document.getElementById("hiddenDate").value;
    var headerShift = document.getElementById("ddlshift").value;

    // Loop all rows
    document.querySelectorAll("#tblBody tr").forEach(function (row) {

        var dateInput = row.querySelector(".row-date");
        var shiftSelect = row.querySelector(".row-shift");

        if (dateInput) dateInput.value = headerDate;
        if (shiftSelect) shiftSelect.value = headerShift;

    });
}
