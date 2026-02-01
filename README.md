function addRow() {

    var tr = "<tr>";

    // ID NO (generate on click / focus)
    tr += "<td><input name='ID_NO' class='form-control form-control-md' " +
          "onclick='generateId(this)' onfocus='generateId(this)'></td>";

    // TAPHOLE NO
    tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md'>";
    tr += "<option></option>";
    tr += "<option>1</option>";
    tr += "<option>2</option>";
    tr += "<option>3</option>";
    tr += "<option>4</option>";
    tr += "</select></td>";

    // DATE TIME
    tr += "<td><input name='DATE_TIME' class='form-control form-control-md'></td>";

    // HH
    tr += "<td><select name='HH' class='form-select form-select-md'>";
    tr += "<option></option>";
    for (var h = 0; h < 24; h++) {
        tr += "<option>" + (h < 10 ? "0" : "") + h + "</option>";
    }
    tr += "</select></td>";

    // MM
    tr += "<td><select name='MM' class='form-select form-select-md'>";
    tr += "<option></option>";
    for (var m = 0; m <= 55; m += 5) {
        tr += "<option>" + (m < 10 ? "0" : "") + m + "</option>";
    }
    tr += "</select></td>";

    // TAPHOLE LENGTH
    tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md'></td>";

    // CLAY PUSHED
    tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md'></td>";

    // TYPE
    tr += "<td><select name='TYPE' class='form-select form-select-md'>";
    tr += "<option></option>";
    tr += "<option>BLEEDING HOLE</option>";
    tr += "<option>HOLE THROUGH</option>";
    tr += "<option>BLANK PUSH</option>";
    tr += "</select></td>";

    tr += "</tr>";

    $("#exception_cast tbody").append(tr);
}
