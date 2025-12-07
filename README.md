$(document).ready(function () {

    // When any row inside both tables is clicked
    $(document).on("click", ".taphole-row, .drilling-row", function () {

        // Remove highlight from all rows in both tables
        $(".taphole-row, .drilling-row").removeClass("highlight");

        // Get clicked row cast no
        let castNo = $(this).data("castno");

        // Highlight same cast no rows in both tables
        $('.taphole-row[data-castno="' + castNo + '"]').addClass("highlight");
        $('.drilling-row[data-castno="' + castNo + '"]').addClass("highlight");
    });

});