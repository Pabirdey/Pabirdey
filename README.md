<h4>Tap Hole Details / Hot Metal</h4>
<table id="tapHoleTable" border="1">
    <thead>
        <tr>
            <th>Cast No</th>
            <th>Trough No</th>
            <th>Cast Start</th>
            <th>Cast End</th>
            <th>Cutko</th>
            <th>Cast Duration</th>
            <th>Casting Rate</th>
            <th>TLC</th>
            <th>EM Weight</th>
            <!-- add more columns if needed -->
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><input name="CastNo" value="55766" /></td>
            <td><input name="TroughNo" value="1" /></td>
            <td><input name="CastStart" value="07:00" /></td>
            <td><input name="CastEnd" value="09:40" /></td>
            <td><input name="Cutko" value="160" /></td>
            

<button onclick="saveTapHoleData()">💾 Save Tap Hole Data</button>

<script>
function saveTapHoleData() {
    var allData = [];

    // Loop through each row
    var rows = document.querySelectorAll("#tapHoleTable tbody tr");
    rows.forEach(function(row) {
        var inputs = row.querySelectorAll("input");
        var rowData = {};

        inputs.forEach(function(input) {
            var name = input.name;
            var value = input.value.trim();
            rowData[name] = value;
        });

        allData.push(rowData);
    });

    // Send to Controller
    $.ajax({
        url: '/CastHouse/SaveTapHoleBulk',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(allData),
        success: function() {
            alert("✅ Data saved successfully!");
        },
        error: function() {
            alert("❌ Save failed!");
        }
    });
}
</script>

