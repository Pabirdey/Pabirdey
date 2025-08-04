<script>
function saveData() {
    var tapHoleData = [];

    document.querySelectorAll(".TAP_Hot_Metal_Details tbody tr").forEach(row => {
        let inputs = row.querySelectorAll("input");
        let rowData = {};
        inputs.forEach(input => {
            let name = input.name;
            let value = input.value.trim();
            rowData[name] = value;
        });
        tapHoleData.push(rowData);
    });

    $.ajax({
        url: '/CastHouse/SaveDrillSlagSourceWise',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(tapHoleData),
        success: function () {
            alert("✅ Data Saved Successfully!");
        },
        error: function () {
            alert("❌ Error saving data.");
        }
    });
}
</script>

<button type="button" class="btn btn-primary w-100" onclick="saveData()">Save</button>
