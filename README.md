<script>

$(document).ready(function () {

    // Call function when dropdown changes
    $("#ddlFurnaceModal").change(function () {
        var furnace = $(this).val();
        loadFurnaceData(furnace);
    });

});


// ✅ Separate reusable function
function loadFurnaceData(furnace) {

    $.ajax({
        url: '/YourController/GetFurnaceData',
        type: 'GET',
        data: { furNo: furnace },
        success: function (data) {

            if (data != null) {
                $("#txtCoalType").val(data.COAL_TYPE || "");
                $("#txtIOType").val(data.IO_TYPE || "");
                $("#txtPyroType").val(data.PYROXINITE_TYPE || "");
                $("#txtLimeType").val(data.LIMESTONE_TYPE || "");
            }
            else {
                clearFurnaceFields();
            }
        },
        error: function (xhr, status, error) {
            console.log(error);
        }
    });

}


// ✅ Optional clear function (clean practice)
function clearFurnaceFields() {
    $("#txtCoalType").val("");
    $("#txtIOType").val("");
    $("#txtPyroType").val("");
    $("#txtLimeType").val("");
}

</script>

