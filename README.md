function generateId(inputBox) {

    // Prevent re-generating if already exists
    if ($(inputBox).val() !== "") {
        return;
    }

    $.ajax({
        url: '@Url.Action("GetNextExceptionCastId", "CastHouse")',
        type: 'GET',
        success: function (data) {
            $(inputBox).val(data);
        },
        error: function () {
            alert("Error generating ID");
        }
    });
}
