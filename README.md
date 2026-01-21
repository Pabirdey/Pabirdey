<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Auto Row + Scroll</title>

<!-- Bootstrap -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

<style>
    body {
        background: #f2f2f2;
    }

    .table-wrapper {
        max-height: 260px;      /* 4 rows visible */
        overflow-y: auto;       /* vertical scroll */
        overflow-x: hidden;
    }

    table input, table select {
        width: 100%;
        text-align: center;
    }

    th {
        position: sticky;
        top: 0;
        background: #dee2e6;
        z-index: 2;
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
            <div class="table-wrapper">
                <table class="table table-bordered text-center" id="exceptionTable">
                    <thead>
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
                        <!-- 4 Default Rows -->
                        <tr></tr>
                        <tr></tr>
                        <tr></tr>
                        <tr></tr>
                    </tbody>
                </table>
            </div>

            <button class="btn btn-primary mt-2 float-end">Save</button>
        </div>
    </div>
</div>

<script>
// Create default rows
document.querySelectorAll("#exceptionTable tbody tr").forEach(r => fillRow(r));

// Down arrow logic
document.addEventListener("keydown", function (e) {

    if (e.key === "ArrowDown") {

        let tbody = document.querySelector("#exceptionTable tbody");
        let rows = tbody.querySelectorAll("tr");
        let active = document.activeElement;

        if (!active || !active.closest("tr")) return;

        let currentRow = active.closest("tr");
        let lastRow = rows[rows.length - 1];

        if (currentRow === lastRow) {
            let newRow = document.createElement("tr");
            fillRow(newRow);
            tbody.appendChild(newRow);

            // Scroll to bottom
            document.querySelector(".table-wrapper").scrollTop =
                document.querySelector(".table-wrapper").scrollHeight;

            newRow.querySelector("input, select").focus();
        }
    }
});

// Function to fill row cells
function fillRow(row) {
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
}
</script>

</body>
</html>