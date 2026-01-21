<script>
document.addEventListener("DOMContentLoaded", function () {

    let tbody = document.querySelector("#exception_cast tbody");

    // Create minimum 4 rows
    for (let i = 0; i < 4; i++) {
        addRow();
    }
});

// Down arrow key event
document.addEventListener("keydown", function (e) {

    if (e.key === "ArrowDown") {

        let active = document.activeElement;
        if (!active || !active.closest("#exception_cast tbody tr")) return;

        let tbody = document.querySelector("#exception_cast tbody");
        let rows = tbody.querySelectorAll("tr");
        let currentRow = active.closest("tr");
        let lastRow = rows[rows.length - 1];

        // If cursor is in last row → add new row
        if (currentRow === lastRow) {
            addRow();

            // Auto scroll to bottom
            let wrapper = document.querySelector(".scrollable-table");
            wrapper.scrollTop = wrapper.scrollHeight;

            // Focus first field of new row
            tbody.lastElementChild.querySelector("input, select").focus();
        }
    }
});

// Function to add row
function addRow() {

    let tbody = document.querySelector("#exception_cast tbody");
    let tr = document.createElement("tr");

    tr.innerHTML = `
        <td><input type="text" class="form-control form-control-sm"></td>
        <td><input type="text" class="form-control form-control-sm"></td>
        <td><input type="datetime-local" class="form-control form-control-sm"></td>
        <td>
            <select class="form-select form-select-sm">
                <option></option>
                ${createOptions(0,23)}
            </select>
        </td>
        <td>
            <select class="form-select form-select-sm">
                <option></option>
                <option>00</option><option>15</option><option>30</option><option>45</option>
            </select>
        </td>
        <td><input type="text" class="form-control form-control-sm"></td>
        <td><input type="text" class="form-control form-control-sm"></td>
        <td>
            <select class="form-select form-select-sm">
                <option></option>
                <option>A</option>
                <option>B</option>
            </select>
        </td>
    `;

    tbody.appendChild(tr);
}

// HH24 dropdown values
function createOptions(start, end) {
    let opt = "";
    for (let i = start; i <= end; i++) {
        opt += `<option>${String(i).padStart(2, '0')}</option>`;
    }
    return opt;
}

// Dummy save function
function saveExceptionCast() {
    alert("Save clicked (AJAX logic can be added)");
}
</script>