  function SaveCastHouseData() {
            debugger;

            // Collect table rows data
             var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr");
            //var rows = document.querySelectorAll("#Driling_Slag_Details tbody tr");
            var CastHouse = [];
            rows.forEach(function (row) {
                var rowData = {};
                var inputs = row.querySelectorAll("input, select");
                inputs.forEach(function (input) {
                    // Trim spaces from each value
                    rowData[input.name] = input.value.trim();
                });
                CastHouse.push(rowData);
            });

            // Trim date and furnace values too
            var selectedDate = document.getElementById("tbFDatePick").value.trim();
            var selectedFurnace = document.getElementById("lstFur").value.trim();

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
                    data: CastHouse,
                    Fdate: selectedDate,
                    Fur: selectedFurnace
                }),
                success: function (response) {
                    if (response.success) {
                        Swal.fire({
                            icon: 'success',
                            text: 'Data Saved successfully!',
                            showConfirmButton: true,
                            customClass: {
                                popup: 'my-swal-popup',   // Popup box
                                title: 'my-swal-title',   // Title text
                                htmlContainer: 'my-swal-text' // Text body
                            }
                        });
                    } else {
                        Swal.fire({
                            icon: 'error',
                            title: '❌ Failed!',
                            text: 'Data could not be saved. Please try again.'
                        });
                    }
                },
                error: function () {
                    Swal.fire({
                        icon: 'error',
                        title: '🚫 Error!',
                        text: 'Something went wrong while saving.'
                    });
                }
            });
        }
