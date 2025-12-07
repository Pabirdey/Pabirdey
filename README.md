$(document).on("click", "#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr", function () {

    let castNo = $(this).data("castno");   // ← correct
    if (!castNo) return;

    // Remove all highlights
    $("#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr").removeClass("highlight");

    // Highlight matching rows
    $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
    $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
});