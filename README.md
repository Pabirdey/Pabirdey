<script>
function saveTapHoleData() {
    var rows = document.querySelectorAll("#tap_hole_table tbody tr");
    var data = [];

    rows.forEach(function(row) {
        var rowData = {};
        var inputs = row.querySelectorAll("input, select");

        inputs.forEach(function(input) {
            rowData[input.name] = input.value;
        });

        data.push(rowData);
    });

    // Get date and furnace values
    var selectedDate = document.getElementById("selectedDate").value;
    var selectedFurnace = document.getElementById("selectedFurnace").value;

    // Create one object to send
    var postData = {
        date: selectedDate,
        furnace: selectedFurnace,
        rows: data
    };

    $.ajax({
        url: '/CastHouse/SaveData', // Your controller
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(postData),
        success: function (res) {
            alert("Saved successfully!");
        },
        error: function () {
            alert("Save failed.");
        }
    });
}
</script>
