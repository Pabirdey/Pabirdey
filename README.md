$(document).on("click", ".castTable tr", function () {

    let castNo = $(this).attr("data-castno");
    if (!castNo) return;

    castNo = castNo.trim();

    // Remove previous highlight from all tables
    $(".castTable tr").removeClass("highlight");

    // Highlight all rows having same cast no
    $('.castTable tr[data-castno="' + castNo + '"]').addClass("highlight");
});