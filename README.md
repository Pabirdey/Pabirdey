function SaveCastHouseData() {
    debugger;

    // Collect table rows data
    var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr");
    var CastHouse = [];
    rows.forEach(function(row) {
        var rowData = {};
        var inputs = row.querySelectorAll("input, select");
        inputs.forEach(function(input) {
            rowData[input.name] = input.value;
        });
        CastHouse.push(rowData);
    });

    var selectedDate = document.getElementById("tbFDatePick").value;
    var selectedFurnace = document.getElementById("lstFur").value;

    // Debug check
    console.log(CastHouse);
    console.log(selectedDate);
    console.log(selectedFurnace);

    // Send AJAX request
    $.ajax({
        url: '/CastHouse/SaveCastHouseData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify({
            data: CastHouse,   // matches the C# parameter name
            Fdate: selectedDate,
            Fur: selectedFurnace
        }),
        success: function(res) {
            alert("Saved successfully!");
        },
        error: function() {
            alert("Save failed.");
        }
    });
}
