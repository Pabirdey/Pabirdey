<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #eef3f9;
            padding: 20px;
        }
        .card {
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        h4 {
            text-align: center;
            margin-bottom: 15px;
        }
        table input {
            height: 28px;
        }
    </style>
</head>

<body>

<h4>Furnace High Line Log Sheet</h4>

<!-- 🔷 TOP TABLE -->
<div class="card">
    <h5>Coke Unloading</h5>

    <table class="table table-bordered" id="mainTable">
        <thead class="table-primary">
            <tr>
                <th>Date</th>
                <th>Shift</th>
                <th>Bunker</th>
            </tr>
        </thead>

        <tbody>

            <!-- Row 1 -->
            <tr>
                <td><input type="text" value="03/05/2026" class="form-control"></td>

                <td>
                    <select class="form-control">
                        <option>A</option>
                        <option>B</option>
                    </select>
                </td>

                <td>
                    <select class="form-control bunker" onchange="updateTonnage()">
                        <option value="">--Select--</option>
                        <option>WESTERN</option>
                        <option>MIDDLE</option>
                        <option>EASTERN</option>
                        <option>H/S NC</option>
                        <option>ST COKE</option>
                    </select>
                </td>
            </tr>

            <!-- Row 2 -->
            <tr>
                <td><input type="text" value="03/05/2026" class="form-control"></td>

                <td>
                    <select class="form-control">
                        <option>A</option>
                        <option>B</option>
                    </select>
                </td>

                <td>
                    <select class="form-control bunker" onchange="updateTonnage()">
                        <option value="">--Select--</option>
                        <option>WESTERN</option>
                        <option>MIDDLE</option>
                        <option>EASTERN</option>
                        <option>H/S NC</option>
                        <option>ST COKE</option>
                    </select>
                </td>
            </tr>

            <!-- Row 3 -->
            <tr>
                <td><input type="text" value="03/05/2026" class="form-control"></td>

                <td>
                    <select class="form-control">
                        <option>A</option>
                        <option>B</option>
                    </select>
                </td>

                <td>
                    <select class="form-control bunker" onchange="updateTonnage()">
                        <option value="">--Select--</option>
                        <option>WESTERN</option>
                        <option>MIDDLE</option>
                        <option>EASTERN</option>
                        <option>H/S NC</option>
                        <option>ST COKE</option>
                    </select>
                </td>
            </tr>

        </tbody>
    </table>
</div>

<!-- 🔷 TONNAGE OF COKE -->
<div class="card">
    <h5>Tonnage of Coke</h5>

    <table class="table table-bordered" id="cokeTable">
        <thead class="table-success">
            <tr>
                <th>Bunker</th>
                <th>C-BF</th>
                <th>E-BF</th>
                <th>F-BF</th>
                <th>Total</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- 🔷 TONNAGE OF NUT COKE -->
<div class="card">
    <h5>Tonnage of Nut Coke</h5>

    <table class="table table-bordered" id="nutTable">
        <thead class="table-warning">
            <tr>
                <th>Bunker</th>
                <th>C-BF</th>
                <th>E-BF</th>
                <th>F-BF</th>
                <th>Total</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- 🔷 SCRIPT -->
<script>

function updateTonnage() {

    let bunkers = [];

    // Collect unique bunker values
    document.querySelectorAll(".bunker").forEach(el => {
        let val = el.value.trim();
        if (val !== "" && !bunkers.includes(val)) {
            bunkers.push(val);
        }
    });

    // Get table bodies
    let cokeBody = document.querySelector("#cokeTable tbody");
    let nutBody = document.querySelector("#nutTable tbody");

    // Clear old rows
    cokeBody.innerHTML = "";
    nutBody.innerHTML = "";

    // Create rows
    bunkers.forEach(bunker => {

        let row = `
            <tr>
                <td><b>${bunker}</b></td>
                <td><input type="number" class="form-control c"></td>
                <td><input type="number" class="form-control e"></td>
                <td><input type="number" class="form-control f"></td>
                <td><input type="number" class="form-control total" readonly></td>
            </tr>
        `;

        cokeBody.innerHTML += row;
        nutBody.innerHTML += row;
    });

    // Add auto total calculation
    document.querySelectorAll("#cokeTable input, #nutTable input").forEach(input => {
        input.addEventListener("input", calculateTotal);
    });
}

function calculateTotal() {

    let row = this.closest("tr");

    let c = parseFloat(row.querySelector(".c")?.value) || 0;
    let e = parseFloat(row.querySelector(".e")?.value) || 0;
    let f = parseFloat(row.querySelector(".f")?.value) || 0;

    row.querySelector(".total").value = c + e + f;
}

</script>

</body>
</html>