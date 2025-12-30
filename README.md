$(document).on("click", "#Driling_Slag_Details *, #TAP_Hot_Metal_Details *", function () {

    let row = $(this).closest("tr");
    if (!row.length) return;

    let castNo = row.attr("data-castno");
    if (!castNo) return;

    castNo = castNo.trim();

    // Remove previous highlight
    $("#Driling_Slag_Details tr").removeClass("highlight");
    $("#TAP_Hot_Metal_Details tr").removeClass("highlight");

    // Highlight all matching rows in BOTH tables
    $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
    $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
});