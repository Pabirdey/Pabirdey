document.addEventListener("keydown", function (e) {

    if (e.key !== "ArrowDown") return;

    var active = document.activeElement;
    if (!active) return;

    var currentRow = active.closest("#exception_cast tbody tr");
    if (!currentRow) return;

    var tbody = document.querySelector("#exception_cast tbody");
    var rows = tbody.querySelectorAll("tr");
    var lastRow = rows[rows.length - 1];

    // ✅ If ArrowDown pressed in LAST ROW → add new row
    if (currentRow === lastRow) {

        addRow();

        // scroll to bottom
        var wrapper = document.querySelector(".scrollable-table");
        if (wrapper) {
            wrapper.scrollTop = wrapper.scrollHeight;
        }

        // focus first input/select of new row
        tbody.lastElementChild.querySelector("input, select").focus();

        // prevent default arrow behavior
        e.preventDefault();
    }
});
