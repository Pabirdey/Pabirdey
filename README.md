<!-- Hidden declared date -->
<span id="lsSelectedFDate" style="display:none;">31/01/2026</span>

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

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
/* =================== Generate ID on click =================== */
function generateId(inputBox) {
    if ($(inputBox).val() !== "") return; // already filled

    $.ajax({
        url: '@Url.Action("GetNextExceptionCastId", "CastHouse")',
        type: 'GET',
        success: function(data) {
            $(inputBox).val(data);
        },
        error: function() {
            alert("Error generating ID");
        }
    });
}

/* =================== Set declared date on click =================== */
function setDeclaredDate(dateInput) {
    if ($(dateInput).val() !== "") return;

    let declaredDate = $('#lsSelectedFDate').text().trim();
    if (declaredDate != "") {
        $(dateInput).val(declaredDate);
    }
}

/* =================== Add Row =================== */
function addRow() {
    var tr = "<tr>";

    tr += "<td><input name='ID_NO' class='form-control form-control-md' autocomplete='off' onclick='generateId(this)'></td>";
    tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'><option></option><option>1</option><option>2</option><option>3</option><option>4</option></select></td>";
    tr += "<td><input name='DATE_TIME' class='form-control form-control-md' autocomplete='off' onclick='setDeclaredDate(this)'></td>";

    tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
    for (var h = 0; h < 24; h++) tr += "<option>" + (h < 10 ? "0" : "") + h + "</option>";
    tr += "</select></td>";

    tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
    for (var m = 0; m <= 55; m += 5) tr += "<option>" + (m < 10 ? "0" : "") + m + "</option>";
    tr += "</select></td>";

    tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md' autocomplete='off'></td>";
    tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md' autocomplete='off'></td>";

    tr += "<td><select name='TYPE' class='form-select form-select-md'><option></option>";
    tr += "<option>BLEEDING HOLE</option><option>HOLE THROUGH</option><option>BLANK PUSH</option></select></td>";

    tr += "</tr>";

    $("#exception_cast tbody").append(tr);
}

/* =================== Display Data =================== */
function Display_Exception_Cast(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Exception_Cast","CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function(result) {
            var parsedData = JSON.parse(result);
            var tbody = $("#exception_cast tbody");
            tbody.empty();
            var rowCount = 0;

            try {
                if (!parsedData[0].ID_NO) throw "no data";
            } catch (e) {
                // no data → 4 blank rows
                addRow(); addRow(); addRow(); addRow();
                return;
            }

            // data found
            for (var i = 0; ; i++) {
                var r = parsedData[i];
                if (!r) break;
                rowCount++;

                var tr = "<tr>";
                tr += "<td><input name='ID_NO' class='form-control form-control-md' autocomplete='off' value='" + (r.ID_NO || "") + "' onclick='generateId(this)'></td>";
                tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'><option></option>";
                for (var t = 1; t <= 4; t++) {
                    tr += "<option " + (r.TAPHOLE_NO == t ? "selected" : "") + ">" + t + "</option>";
                }
                tr += "</select></td>";
                tr += "<td><input name='DATE_TIME' class='form-control form-control-md' autocomplete='off' value='" + (r.DATE_TIME || "") + "' onclick='setDeclaredDate(this)'></td>";

                tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
                for (var h = 0; h < 24; h++) tr += "<option " + (r.HH == h ? "selected" : "") + ">" + (h < 10 ? "0" : "") + h + "</option>";
                tr += "</select></td>";

                tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
                for (var m = 0; m <= 55; m += 5) tr += "<option " + (r.MM == m ? "selected" : "") + ">" + (m < 10 ? "0" : "") + m + "</option>";
                tr += "</select></td>";

                tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md' autocomplete='off' value='" + (r.TAPHOLE_LENGTH || "") + "'></td>";
                tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md' autocomplete='off' value='" + (r.CLAY_PUSHED || "") + "'></td>";

                tr += "<td><select name='TYPE' class='form-select form-select-md'><option></option>";
                tr += "<option " + (r.TYPE == 'BLEEDING HOLE' ? "selected" : "") + ">BLEEDING HOLE</option>";
                tr += "<option " + (r.TYPE == 'HOLE THROUGH' ? "selected" : "") + ">HOLE THROUGH</option>";
                tr += "<option " + (r.TYPE == 'BLANK PUSH' ? "selected" : "") + ">BLANK PUSH</option></select></td>";

                tr += "</tr>";
                tbody.append(tr);
            }

            // ensure minimum 4 rows
            while (rowCount < 4) {
                addRow();
                rowCount++;
            }
        }
    });
}

/* =================== Add row on ArrowDown if last row =================== */
document.addEventListener("keydown", function(e) {
    if (e.key === "ArrowDown") {
        let active = document.activeElement;
        if (!active || !active.closest("#exception_cast tbody tr")) return;

        let tbody = document.querySelector("#exception_cast tbody");
        let rows = tbody.querySelectorAll("tr");
        let currentRow = active.closest("tr");
        let lastRow = rows[rows.length - 1];

        if (currentRow === lastRow) {
            addRow();
            let wrapper = document.querySelector(".scrollable-table");
            wrapper.scrollTop = wrapper.scrollHeight;
            tbody.lastElementChild.querySelector("input, select").focus();
        }
    }
});
</script>
