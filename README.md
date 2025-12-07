#TAP_Hot_Metal_Details tr.highlight td {
    background-color: yellow !important;
}
$(document).on("click", "#TAP_Hot_Metal_Details *", function () {

    let row = $(this).closest("tr"); // Get the parent row

    if (!row.length) return;

    let castNo = row.attr("data-castno");
    if (!castNo) return;

    castNo = castNo.trim();

    // Remove previous highlight
    $("#TAP_Hot_Metal_Details tr").removeClass("highlight");

    // Highlight the row
    row.addClass("highlight");
});
