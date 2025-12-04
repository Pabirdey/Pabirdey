// Event delegation for dynamically created rows
$(document).on("change", "select[name='MG_CLAY_USED']", function () {

    if ($(this).val() === "OTHERS") {

        // save reference of current dropdown
        window.currentClayDropdown = this;

        // open modal
        var modal = new bootstrap.Modal(document.getElementById("othersModal"));
        modal.show();
    }
});