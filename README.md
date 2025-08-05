<script>
    function saveCarbonData() {
        var formData = [];

        var tableRows = document.querySelectorAll("#carbonPasteTable tbody tr");

        tableRows.forEach(function (row) {
            var rowData = {
                DateTime: row.querySelector("input[name='DateTime']").value,
                Shift: row.querySelector("input[name='Shift']").value,
                BelowTuyere: row.querySelector("input[name='BelowTuyere']").value,
                NoOfDrum: row.querySelector("input[name='NoOfDrum']").value
            };
            formData.push(rowData);
        });

        $.ajax({
            url: '/CastHouse/SaveCarbonPasteData', // Adjust controller name if needed
            type: 'POST',
            data: { jsonData: JSON.stringify(formData) },
            success: function (res) {
                alert("Data saved successfully!");
            },
            error: function (err) {
                alert("Error saving data");
            }
        });
    }
</script>