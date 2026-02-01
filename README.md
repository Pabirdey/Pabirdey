document.addEventListener("click", function (e) {

    var row = e.target.closest("#exception_cast tbody tr");
    if (!row) return;

    var tbody = document.querySelector("#exception_cast tbody");
    var rows = tbody.querySelectorAll("tr");
    var lastRow = rows[rows.length - 1];

    // ✅ If clicked row is LAST ROW → add new row
    if (row === lastRow) {

        addRow();

        // auto scroll to bottom
        var wrapper = document.querySelector(".scrollable-table");
        if (wrapper) {
            wrapper.scrollTop = wrapper.scrollHeight;
        }

        // focus first input of new row
        tbody.lastElementChild.querySelector("input, select").focus();
    }
});
