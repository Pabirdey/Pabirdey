<script>
    function saveCarbonPaste() {
        var formData = [];
        var tableRows = document.querySelectorAll("#carbon_paste_inj tbody tr");
        tableRows.forEach(function (row) {
            var rowData = {
                DateTime: row.querySelector("input[name='DateTime']").value,
                Shift: row.querySelector("input[name='Shift']").value,
                BelowTuyere: row.querySelector("input[name='BelowTuyere']").value,
                NoOfDrum: row.querySelector("input[name='NoOfDrum']").value
            };
            formData.push(rowData);
        });

        // 👇 Get date and source
        var selectedDate = document.getElementById("selectedDate").value;
        var selectedSource = document.getElementById("selectedSource").value;

        $.ajax({
            url: '/CastHouse/SaveCarbonPasteData',
            type: 'POST',
            data: {
                jsonData: JSON.stringify(formData),
                date: selectedDate,
                source: selectedSource
            },
            success: function (res) {
                alert("Data saved successfully!");
            },
            error: function () {
                alert("Error saving data");
            }
        });
    }
</script>
