<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Mudgun Clay Details</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

<style>
.input-wrapper {
    position: relative;
}
.arrow-btn {
    position: absolute;
    right: 10px;
    top: 8px;
    cursor: pointer;
}
.list-box {
    border: 1px solid #ccc;
    display: none;
    background: #fff;
    position: absolute;
    z-index: 1000;
    width: 100%;
}
.list-box div {
    padding: 5px;
    cursor: pointer;
}
.list-box div:hover {
    background: #0d6efd;
    color: #fff;
}
</style>
</head>

<body class="p-4">

<h4 class="mb-3">Mudgun Details</h4>

<table class="table table-bordered" id="Mudgun_Details">
    <thead class="table-dark">
        <tr>
            <th>CAST NO</th>
            <th>MG CLAY USED</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>

<!-- ================= MODAL ================= -->
<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title w-100 text-center">Clay Weightage</h5>
                <button class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">

                <!-- Clay 1 -->
                <div class="row mb-3">
                    <div class="col-2">Clay1</div>
                    <div class="col-7">
                        <select class="form-select" id="clay1">
                            <option value="">Select</option>
                            <option value="CLAY_A">Clay A</option>
                            <option value="CLAY_B">Clay B</option>
                        </select>
                    </div>
                    <div class="col-3">
                        <input type="number" class="form-control" id="clay1_pct" placeholder="%">
                    </div>
                </div>

                <!-- Clay 2 -->
                <div class="row mb-3">
                    <div class="col-2">Clay2</div>
                    <div class="col-7">
                        <select class="form-select" id="clay2">
                            <option value="">Select</option>
                            <option value="CLAY_A">Clay A</option>
                            <option value="CLAY_B">Clay B</option>
                        </select>
                    </div>
                    <div class="col-3">
                        <input type="number" class="form-control" id="clay2_pct" placeholder="%">
                    </div>
                </div>

                <!-- Clay 3 -->
                <div class="row">
                    <div class="col-2">Clay3</div>
                    <div class="col-7">
                        <select class="form-select" id="clay3">
                            <option value="">Select</option>
                            <option value="CLAY_A">Clay A</option>
                            <option value="CLAY_B">Clay B</option>
                        </select>
                    </div>
                    <div class="col-3">
                        <input type="number" class="form-control" id="clay3_pct" placeholder="%">
                    </div>
                </div>

            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" onclick="saveClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<script>
let currentClayRowIndex = null;

/* ================= AJAX PART ================= */
function Display_Mudgun_Details() {

    // 🔹 Simulated AJAX result (replace with MVC AJAX)
    let parsedData = [
        { CAST_NO: "1001", MG_CLAY_USED: "" },
        { CAST_NO: "1002", MG_CLAY_USED: "" }
    ];

    let html = "";

    parsedData.forEach((row, i) => {

        html += `
        <tr>
            <td>
                <input class="form-control" value="${row.CAST_NO}" readonly>
            </td>

            <td>
                <div class="input-wrapper">
                    <input type="text" class="form-control" id="clayInput_${i}">
                    <div class="arrow-btn" onclick="toggleList(${i})">▼</div>

                    <div class="list-box" id="list_${i}">
                        <div onclick="selectItem(this, ${i})">ACE</div>
                        <div onclick="selectItem(this, ${i})">BRL</div>
                        <div onclick="selectItem(this, ${i})">LRH</div>
                        <div onclick="selectItem(this, ${i})">OTHERS</div>
                    </div>
                </div>
            </td>
        </tr>`;
    });

    document.querySelector("#Mudgun_Details tbody").innerHTML = html;
}

window.onload = Display_Mudgun_Details;

/* ================= DROPDOWN ================= */
function toggleList(index) {
    document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");
    document.getElementById("list_" + index).style.display = "block";
}

function selectItem(el, index) {

    event.stopPropagation();

    let val = el.innerText.trim();
    document.getElementById("clayInput_" + index).value = val;
    document.getElementById("list_" + index).style.display = "none";

    if (val === "OTHERS") {
        currentClayRowIndex = index;
        clay1.value = clay2.value = clay3.value = "";
        clay1_pct.value = clay2_pct.value = clay3_pct.value = "";
        new bootstrap.Modal(clayModal).show();
    }
}

/* ================= SAVE MODAL ================= */
function saveClay() {

    let c1 = clay1.value, c2 = clay2.value, c3 = clay3.value;
    let p1 = +clay1_pct.value || 0;
    let p2 = +clay2_pct.value || 0;
    let p3 = +clay3_pct.value || 0;

    if (!c1 && !c2 && !c3) {
        alert("Select at least one clay");
        return;
    }

    if (p1 + p2 + p3 !== 100) {
        alert("Total percentage must be 100");
        return;
    }

    let result = [];
    if (c1) result.push(`${c1}(${p1}%)`);
    if (c2) result.push(`${c2}(${p2}%)`);
    if (c3) result.push(`${c3}(${p3}%)`);

    document.getElementById("clayInput_" + currentClayRowIndex).value =
        result.join(" + ");

    bootstrap.Modal.getInstance(clayModal).hide();
}

/* ================= CLOSE LIST ================= */
document.addEventListener("click", () => {
    document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");
});
</script>

</body>
</html>
