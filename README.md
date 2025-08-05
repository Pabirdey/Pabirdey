<button type="button" class="btn btn-warning w-100" onclick="saveTapHoleData()">Save</button>
    function saveTapHoleData() {
                var allData = [];

                // Loop through each row
                var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr");
                rows.forEach(function (row) {
                    var inputs = row.querySelectorAll("input");
                    var rowData = {};

                    inputs.forEach(function (input) {
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
                    success: function () {
                        alert("✅ Data saved successfully!");
                    },
                    error: function () {
                        alert("❌ Save failed!");
                    }
                });
            }
