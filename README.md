function createRow() {
    return `
    <tr>
        <td><input type="date" class="form-control"></td>

        <td>
            <select class="form-control" style="height:30px;">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>

        <!-- ✅ 3rd column dropdown -->
        <td>
            <select class="form-control" style="height:30px;">
                <option value="">--Select--</option>
                <option value="X">X</option>
                <option value="Y">Y</option>
                <option value="Z">Z</option>
            </select>
        </td>

        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
        <td><input class="form-control total" readonly></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
    </tr>`;
}

// generate rows
for (let i = 0; i < 9; i++) {
    document.getElementById("tblBody").innerHTML += createRow();
}
