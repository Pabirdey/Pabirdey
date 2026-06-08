$(document).ready(function () {

    var now = new Date();
    var hour = now.getHours();

    $("#ddlshift").val(
        hour >= 22 || hour < 6 ? "C" :
        hour >= 14 ? "B" : "A"
    );

    if (hour < 6)
        now.setDate(now.getDate() - 1);

    $("#txtDate").val(now.toLocaleDateString('en-GB'));
});