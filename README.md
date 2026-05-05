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
