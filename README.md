<div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
    <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
        <thead class="table-secondary sticky-top">
            <tr>
                <th style="width:150px;">ID No</th>
                <th style="width:50px;">TAPHOLE No</th>
                <th style="width:180px;">Date</th>
                <th style="width:90px;">HH24</th>
                <th style="width:90px;">MM</th>
                <th>Taphole Length</th>
                <th>Clay Paused</th>
                <th style="width:240px;">Type</th>
            </tr>
        </thead>
        <tbody>
            <!-- rows created by JS -->
        </tbody>
    </table>
</div>

<script>
// ======================== Generate ID ========================
function generateId(inputBox) {
    // Only generate if empty
    if ($(inputBox).val() !== "") return;

    $.ajax({
        url: '@Url.Action("GetNextExceptionCastId", "CastHouse")',
        type: 'GET',
        success: function (data) {
            $(inputBox).val(data);
        },
        error: function () {
            alert("Error generating ID");
        }
    });
}

// ======================== Add Row ===========================
function addRow() {
    var tr = "<tr>";
    tr += "<td><input name='ID_NO' class='form-control form-control-md'></td>"; // ID generation handled below
    tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'>";
    tr += "<option></option><option>1</option><option>2</option><option>3</option><option>4</option></select></td>";
    tr += "<td><input name='DATE_TIME' class='form-control form-control-md'></td>";
    tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
    for (var h = 0; h < 24; h++) tr += "<option>" + (h < 10 ? "0" : "") + h + "</option>";
    tr += "</select></td>";
    tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
    for (var m = 0; m <= 55; m += 5) tr += "<option>" + (m < 10 ? "0" : "") + m + "</option>";
    tr += "</select></td>";
    tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md'></td>";
    tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md'></td>";
    tr += "<td><select name='TYPE' class='form-select form-select-md'><option></option>";
    tr += "<option>BLEEDING HOLE</option><option>HOLE THROUGH</option><option>BLANK PUSH</option>";
    tr += "</select></td>";
    tr += "</tr>";

    $("#exception_cast tbody").append(tr);
}

// ======================== Display Data ======================
function Display_Exception_Cast(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Exception_Cast","CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Exception_Cast) {
            var parsedData = JSON.parse(result_Exception_Cast);
            var tbody = $("#exception_cast tbody");
            tbody.empty();
            var rowCount = 0;

            try {
                var chk = parsedData[0].ID_NO;
            } catch (e) {
                // No data → add 4 blank rows
                addRow(); addRow(); addRow(); addRow();
                return;
            }

            // Data found
            for (var i = 0; ; i++) {
                var r = parsedData[i];
                if (!r) break;
                rowCount++;

                var tr = "<tr>";
                tr += "<td><input name='ID_NO' class='form-control form-control-md' value='" + (r.ID_NO || "") + "'></td>";
                tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'>";
                tr += "<option></option>";
                for (var t = 1; t <= 4; t++) {
                    tr += "<option " + (r.TAPHOLE_NO == t ? "selected" : "") + ">" + t + "</option>";
                }
                tr += "</select></td>";
                tr += "<td><input name='DATE_TIME' class='form-control form-control-md' value='" + (r.DATE_TIME || "") + "'></td>";
                tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
                for (var h = 0; h < 24; h++) tr += "<option " + (r.HH == h ? "selected" : "") + ">" + (h < 10 ? "0" : "") + h + "</option>";
                tr += "</select></td>";
                tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
                for (var m = 0; m <= 55; m += 5) tr += "<option " + (r.MM == m ? "selected" : "") + ">" + (m < 10 ? "0" : "") + m + "</option>";
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

            // Ensure minimum 4 rows
            while (rowCount < 4) {
                addRow();
                rowCount++;
            }
        }
    });
}

// ======================== Event Delegation ==================
// Generate ID only when clicking ID_NO cell
$(document).on("click", "#exception_cast tbody input[name='ID_NO']", function () {
    generateId(this);
});

// Add new row if ArrowDown pressed on last row
document.addEventListener("keydown", function (e) {
    if (e.key === "ArrowDown") {
        let active = document.activeElement;
        if (!active || !active.closest("#exception_cast tbody tr")) return;

        let tbody = document.querySelector("#exception_cast tbody");
        let rows = tbody.querySelectorAll("tr");
        let currentRow = active.closest("tr");
        let lastRow = rows[rows.length - 1];

        if (currentRow === lastRow) {
            addRow();
            // scroll to bottom
            let wrapper = document.querySelector(".scrollable-table");
            wrapper.scrollTop = wrapper.scrollHeight;
            // focus first input of new row
            tbody.lastElementChild.querySelector("input, select").focus();
        }
    }
});
</script>
