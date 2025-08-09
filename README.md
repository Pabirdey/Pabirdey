<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
function SaveCastHouseData() {
    debugger;

    // Collect table rows data
    var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr");
    var CastHouse = [];

    rows.forEach(function (row) {
        var rowData = {};
        var inputs = row.querySelectorAll("input, select");
        inputs.forEach(function (input) {
            rowData[input.name] = input.value;
        });
        CastHouse.push(rowData);
    });

    var Fdate = $("#Fdate").val();
    var Fur = $("#Fur").val();

    $.ajax({
        url: '/CastHouse/SaveCastHouseData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify({
            data: CastHouse,
            Fdate: Fdate,
            Fur: Fur
        }),
        success: function (response) {
            if (response.success) {
                Swal.fire({
                    icon: 'success',
                    title: '✅ Saved!',
                    text: 'Data has been saved to Oracle successfully.',
                    timer: 2000,
                    showConfirmButton: false
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
