success: function (result_Exception_Cast) {

    var parsedData = JSON.parse(result_Exception_Cast);
    var tbody = $("#exception_cast tbody");
    tbody.empty();

    var rowCount = 0;

    // 🔴 NO DATA
    try {
        var chk = parsedData[0].ID_NO;
    } catch (e) {
        addRow(); addRow(); addRow(); addRow();
        return;
    }

    // 🟢 DATA FOUND
    for (var i = 0; ; i++) {

        var r = parsedData[i];
        if (!r) break;

        rowCount++;

        var tr = "<tr>";

        tr += "<td><input name='ID_NO' class='form-control form-control-md' value='" + (r.ID_NO || "") + "'></td>";

        tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'>";
        tr += "<option></option>";
        tr += "<option " + (r.TAPHOLE_NO == 1 ? "selected" : "") + ">1</option>";
        tr += "<option " + (r.TAPHOLE_NO == 2 ? "selected" : "") + ">2</option>";
        tr += "<option " + (r.TAPHOLE_NO == 3 ? "selected" : "") + ">3</option>";
        tr += "<option " + (r.TAPHOLE_NO == 4 ? "selected" : "") + ">4</option>";
        tr += "</select></td>";

        tr += "<td><input name='DATE_TIME' class='form-control form-control-md' value='" + (r.DATE_TIME || "") + "'></td>";

        tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
        for (var h = 0; h < 24; h++) {
            tr += "<option " + (r.HH == h ? "selected" : "") + ">" + (h < 10 ? "0" : "") + h + "</option>";
        }
        tr += "</select></td>";

        tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
        for (var m = 0; m <= 55; m += 5) {
            tr += "<option " + (r.MM == m ? "selected" : "") + ">" + (m < 10 ? "0" : "") + m + "</option>";
        }
        tr += "</select></td>";

        tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md' value='" + (r.TAPHOLE_LENGTH || "") + "'></td>";
        tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md' value='" + (r.CLAY_PUSHED || "") + "'></td>";

        tr += "<td><select name='TYPE' class='form-select form-select-md'>";
        tr += "<option></option>";
        tr += "<option " + (r.TYPE == 'BLEEDING HOLE' ? "selected" : "") + ">BLEEDING HOLE</option>";
        tr += "<option " + (r.TYPE == 'HOLE THROUGH' ? "selected" : "") + ">HOLE THROUGH</option>";
        tr += "<option " + (r.TYPE == 'BLANK PUSH' ? "selected" : "") + ">BLANK PUSH</option>";
        tr += "</select></td>";

        tr += "</tr>";

        tbody.append(tr);
    }

    // ✅ ENSURE MINIMUM 4 ROWS
    while (rowCount < 4) {
        addRow();
        rowCount++;
    }
}
document.addEventListener("keydown", function (e) {

    if (e.key !== "ArrowDown") return;

    var active = document.activeElement;
    if (!active) return;

    var currentRow = active.closest("#exception_cast tbody tr");
    if (!currentRow) return;

    var tbody = document.querySelector("#exception_cast tbody");
    var rows = tbody.querySelectorAll("tr");
    var lastRow = rows[rows.length - 1];

    // last cell (TYPE dropdown)
    var lastCell = currentRow.querySelector("td:last-child select");

    // ✅ Only when cursor is on LAST ROW + LAST CELL
    if (currentRow === lastRow && active === lastCell) {

        addRow();

        // scroll
        var wrapper = document.querySelector(".scrollable-table");
        if (wrapper) {
            wrapper.scrollTop = wrapper.scrollHeight;
        }

        // focus first field of new row
        tbody.lastElementChild.querySelector("input, select").focus();
    }
});
