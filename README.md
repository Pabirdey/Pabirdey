$(document).on("click", "#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr", function () {

    // Always read data attribute as string
    let castNo = $(this).attr("data-castno");

    if (!castNo) return;
    castNo = castNo.trim();

    // Remove old highlights
    $("#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr").removeClass("highlight");

    // Highlight both tables where CAST NO matches
    $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
    $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
});
