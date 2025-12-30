$(document).on("click", "#Driling_Slag_Details *, #TAP_Hot_Metal_Details *", function () {

    let row = $(this).closest("tr");
    if (!row.length) return;

    let castNo = row.attr("data-castno");
    if (!castNo) return;

    castNo = castNo.trim();

    // Remove previous highlight / active
    $("#Driling_Slag_Details tr, #TAP_Hot_Metal_Details tr")
        .removeClass("highlight active");

    // Highlight + Activate matching rows
    let matchRows = $('#Driling_Slag_Details tr[data-castno="' + castNo + '"], ' +
                     '#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]');

    matchRows.addClass("highlight active");

    // Auto scroll to first matching row
    if (matchRows.length > 0) {
        matchRows[0].scrollIntoView({ behavior: "smooth", block: "center" });
    }
});
.highlight{
    background: yellow;
}
.active{
    outline: 2px solid red;
}