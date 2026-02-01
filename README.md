document.addEventListener("keydown", function (e) {

    if (e.key !== "ArrowDown") return;

    var active = document.activeElement;
    if (!active) return;

    var currentRow = active.closest("#exception_cast tbody tr");
    if (!currentRow) return;

    var tbody = document.querySelector("#exception_cast tbody");
    var rows = tbody.querySelectorAll("tr");
    var lastRow = rows[rows.length - 1];

    // last two editable cells
    var clayCell = currentRow.querySelector("input[name='CLAY_PUSHED']");
    var typeCell = currentRow.querySelector("select[name='TYPE']");

    // ✅ LAST ROW + (CLAY_PUSHED OR TYPE)
    if (
        currentRow === lastRow &&
        (active === clayCell || active === typeCell)
    ) {
        addRow();

        // scroll to bottom
        var wrapper = document.querySelector(".scrollable-table");
        if (wrapper) {
            wrapper.scrollTop = wrapper.scrollHeight;
        }

        // focus first input of new row
        tbody.lastElementChild.querySelector("input, select").focus();
    }
});
