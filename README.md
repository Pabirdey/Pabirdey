// Highlight row when clicking anywhere inside the row
$(document).on("click", "#TAP_Hot_Metal_Details tr, #TAP_Hot_Metal_Details tr *", function () {

    let row = $(this).closest("tr");     // always get parent TR
    let castNo = row.attr("data-castno");

    if (!castNo) return;
    castNo = castNo.trim();

    // Remove previous highlights
    $("#TAP_Hot_Metal_Details tr").removeClass("highlight");

    // Highlight row with same CAST_NO
    $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
});
