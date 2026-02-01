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
