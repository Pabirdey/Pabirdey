function Display_Exception_Cast(lsSelectedFDate, IsSelectedFur) {
            $.ajax({
        url: '@Url.Action("Get_Display_Exception_Cast","CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Exception_Cast) {
            var parsedData = JSON.parse(result_Exception_Cast);
            var tbody = $("#exception_cast tbody");
            tbody.empty();            
            try {
                var chk = parsedData[0].ID_NO;
            } catch (e) {
                addRow();
                addRow();
                addRow();
                addRow();
                return;
            }
            for (var i = 0; ; i++) {
                var r = parsedData[i];
                if (!r) break;

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
        }
    });
}
<script>   
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
    function addRow() {
        var tr = "<tr>";
        tr += "<td><input name='ID_NO' class='form-control form-control-md'></td>";
        tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'>";
        tr += "<option></option><option>1</option><option>2</option><option>3</option><option>4</option>";
        tr += "</select></td>";
        tr += "<td><input name='DATE_TIME' class='form-control form-control-md'></td>";
        tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
        for (var h = 0; h < 24; h++) {
            tr += "<option>" + (h < 10 ? "0" : "") + h + "</option>";
        }
        tr += "</select></td>";
        tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
        for (var m = 0; m <= 55; m += 5) {
            tr += "<option>" + (m < 10 ? "0" : "") + m + "</option>";
        }
        tr += "</select></td>";
        tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md'></td>";
        tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md'></td>";
        tr += "<td><select name='TYPE' class='form-select form-select-md'>";
        tr += "<option></option>";
        tr += "<option>BLEEDING HOLE</option>";
        tr += "<option>HOLE THROUGH</option>";
        tr += "<option>BLANK PUSH</option>";
        tr += "</select></td>";
        tr += "</tr>";
        $("#exception_cast tbody").append(tr);
    }


    </script>
