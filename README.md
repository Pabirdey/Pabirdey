<script>
$(document).ready(function () {

    $("#ddlFurnaceModal").change(function () {

        var furnace = $(this).val();

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
                    $("#txtCoalType").val("");
                    $("#txtIOType").val("");
                    $("#txtPyroType").val("");
                    $("#txtLimeType").val("");
                }

            },
            error: function (xhr, status, error) {
                console.log(error);
            }
        });

    });

});
</script>