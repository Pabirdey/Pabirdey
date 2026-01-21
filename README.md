<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Auto Row Add on Down Arrow</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f5f5f5;
        }

        table input, table select {
            width: 100%;
            text-align: center;
        }

        th {
            font-size: 14px;
        }
    </style>
</head>
<body>

<div class="container mt-4">
    <div class="card shadow">
        <div class="card-header fw-bold">
            Exception Cast Entry
        </div>

        <div class="card-body">
            <table class="table table-bordered text-center" id="exceptionTable">
                <thead class="table-secondary">
                    <tr>
                        <th>Id No</th>
                        <th>Date</th>
                        <th>HH24</th>
                        <th>MM</th>
                        <th>Taphole Length</th>
                        <th>Clay Pushed</th>
                        <th>Type</th>
                    </tr>
                </thead>

                <tbody>
                    <tr>
                        <td><input type="text" class="form-control"></td>
                        <td><input type="date" class="form-control"></td>
                        <td>
                            <select class="form-select">
                                <option></option>
                                <option>00</option><option>01</option><option>02</option>
                                <option>03</option><option>04</option><option>05</option>
                            </select>
                        </td>
                        <td>
                            <select class="form-select">
                                <option></option>
                                <option>00</option><option>15</option><option>30</option><option>45</option>
                            </select>
                        </td>
                        <td><input type="text" class="form-control"></td>
                        <td><input type="text" class="form-control"></td>
                        <td>
                            <select class="form-select">
                                <option></option>
                                <option>A</option>
                                <option>B</option>
                            </select>
                        </td>
                    </tr>
                </tbody>
            </table>

            <button class="btn btn-primary float-end">Save</button>
        </div>
    </div>
</div>

<script>
document.addEventListener("keydown", function (e) {

    if (e.key === "ArrowDown") {

        let table = document.getElementById("exceptionTable");
        let tbody = table.querySelector("tbody");
        let rows = tbody.querySelectorAll("tr");

        let active = document.activeElement;

        if (!active || (active.tagName !== "INPUT" && active.tagName !== "SELECT")) {
            return;
        }

        let currentRow = active.closest("tr");
        let lastRow = rows[rows.length - 1];

        // If cursor is on LAST row → add new row
        if (currentRow === lastRow) {
            addNewRow(tbody);
        }
    }
});

function addNewRow(tbody) {

    let row = document.createElement("tr");

    row.innerHTML = `
        <td><input type="text" class="form-control"></td>
        <td><input type="date" class="form-control"></td>
        <td>
            <select class="form-select">
                <option></option>
                <option>00</option><option>01</option><option>02</option>
                <option>03</option><option>04</option><option>05</option>
            </select>
        </td>
        <td>
            <select class="form-select">
                <option></option>
                <option>00</option><option>15</option><option>30</option><option>45</option>
            </select>
        </td>
        <td><input type="text" class="form-control"></td>
        <td><input type="text" class="form-control"></td>
        <td>
            <select class="form-select">
                <option></option>
                <option>A</option>
                <option>B</option>
            </select>
        </td>
    `;

    tbody.appendChild(row);

    // Auto focus first field of new row
    row.querySelector("input, select").focus();
}
</script>

</body>
</html>