<!DOCTYPE html>
<html>
<head>
    <title>Down Arrow Add Row</title>
    <style>
        table {
            border-collapse: collapse;
            width: 70%;
        }

        th, td {
            border: 1px solid #000;
            padding: 6px;
            text-align: center;
        }

        input, select {
            width: 95%;
            height: 28px;
        }
    </style>
</head>
<body>

<h3>Press ↓ Down Arrow in Last Column to Add Row</h3>

<table id="myTable">
    <thead>
        <tr>
            <th>Sl No</th>
            <th>Item Name</th>
            <th>Type (↓)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td><input type="text"></td>
            <td>
                <select onkeydown="checkDownArrow(event,this)">
                    <option value="">Select</option>
                    <option>A</option>
                    <option>B</option>
                    <option>C</option>
                </select>
            </td>
        </tr>
    </tbody>
</table>

<script>
function checkDownArrow(e, element) {

    // Down Arrow key only (40)
    if (e.keyCode === 40) {

        let table = document.getElementById("myTable");
        let row = element.closest("tr");
        let tbody = table.tBodies[0];

        let rowIndex = row.rowIndex - 1;
        let lastRowIndex = tbody.rows.length - 1;

        let colIndex = element.parentElement.cellIndex;
        let lastColIndex = row.cells.length - 1;

        // LAST ROW + LAST COLUMN
        if (rowIndex === lastRowIndex && colIndex === lastColIndex) {
            e.preventDefault();
            addNewRow(table);
        }
    }
}

function addNewRow(table) {

    let tbody = table.tBodies[0];
    let rowNo = tbody.rows.length + 1;

    let newRow = tbody.insertRow();

    newRow.innerHTML = `
        <td>${rowNo}</td>
        <td><input type="text"></td>
        <td>
            <select onkeydown="checkDownArrow(event,this)">
                <option value="">Select</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>
    `;

    // Focus dropdown of new row
    newRow.querySelector("select").focus();
}
</script>

</body>
</html>