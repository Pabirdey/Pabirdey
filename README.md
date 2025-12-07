$(document).on("click", "#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr", function () {

    let castNo = $(this).attr("data-castno");  // use attr instead of .data()

    if (!castNo || castNo.trim() === "") return;
    castNo = castNo.trim();   // ensure clean value

    // Remove old highlights
    $("#TAP_Hot_Metal_Details tr, #Driling_Slag_Details tr").removeClass("highlight");

    // Highlight rows with same CAST_NO in BOTH tables
    $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
    $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
});
