 function SaveCastHouseData() {
            debugger;
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
            console.log(CastHouse);
            var selectedDate = document.getElementById("tbFDatePick").value;
            var selectedFurnace = document.getElementById("lstFur").value;
            console.log(selectedDate);
            console.log(selectedFurnace);
            $.ajax({
                url: '/CastHouse/SaveCastHouseData',
                type: 'POST',
                contentType: 'application/json',
                CastHouseData: JSON.stringify(CastHouse),
                Fdate:selectedDate,
                Fur:selectedFurnace,
                success: function (res) {
                    alert("Saved successfully!");
                },
                error: function () {
                    alert("Save failed.");
                }
            });
        }
