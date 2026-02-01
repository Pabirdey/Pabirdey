<table class="table table-bordered" id="Mudgun_Details">
    <thead>
        <tr>
            <th>Cast No</th>
            <th>MG Clay Used</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">MG CLAY WEIGHTAGE</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">

                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY1" class="form-select">
                            <option value="">Clay 1</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P1" class="form-select">
                            <option value="">%</option>
                            <option>50</option>
                            <option>100</option>
                        </select>
                    </div>
                </div>

                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY2" class="form-select">
                            <option value="">Clay 2</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P2" class="form-select">
                            <option value="">%</option>
                            <option>20</option>
                            <option>50</option>
                        </select>
                    </div>
                </div>

                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY3" class="form-select">
                            <option value="">Clay 3</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P3" class="form-select">
                            <option value="">%</option>
                            <option>30</option>
                        </select>
                    </div>
                </div>

            </div>

            <div class="modal-footer">
                <button class="btn btn-success" onclick="checkClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>
        </div>
    </div>
</div>
<script>
/* ================= GLOBAL ================= */
let activeMgClayInput = null;

/* ================= LOAD TABLE ================= */
function Display_Mudgun_Details() {

    let parsedData = [
        { CAST_NO: '101', MG_CLAY_USED: '' },
        { CAST_NO: '102', MG_CLAY_USED: '' }
    ];

    let tableBody = "";

    for (let i = 0; i < parsedData.length; i++) {

        tableBody += `
        <tr>
            <td>${parsedData[i].CAST_NO}</td>
            <td>
                <div class="mgClayWrapper">
                    <input type="text"
                           class="form-control form-control-sm mgClayInput"
                           value="${parsedData[i].MG_CLAY_USED}">
                    <button type="button"
                            class="btn btn-sm btn-secondary"
                            onclick="showDropdown(this)">▼</button>

                    <div class="mgClayList" style="display:none;border:1px solid #ccc;">
                        <div onclick="selectClay(this)">ACE</div>
                        <div onclick="selectClay(this)">BRL</div>
                        <div onclick="selectClay(this)">OTHERS</div>
                    </div>
                </div>
            </td>
        </tr>`;
    }

    document.querySelector("#Mudgun_Details tbody").innerHTML = tableBody;
}

/* ================= DROPDOWN ================= */
function showDropdown(btn) {
    document.querySelectorAll(".mgClayList").forEach(d => d.style.display = "none");
    btn.nextElementSibling.style.display = "block";
}

/* ================= SELECT CLAY ================= */
function selectClay(item) {

    let list = item.parentElement;
    let input = list.closest(".mgClayWrapper").querySelector(".mgClayInput");

    if (item.innerText === "OTHERS") {
        activeMgClayInput = input;
        new bootstrap.Modal(document.getElementById("mgClayOtherModal")).show();
    } else {
        input.value = item.innerText;
    }

    list.style.display = "none";
}

/* ================= MODAL SAVE ================= */
function checkClay() {

    let P1 = Number(document.getElementById("P1").value) || 0;
    let P2 = Number(document.getElementById("P2").value) || 0;
    let P3 = Number(document.getElementById("P3").value) || 0;

    let MG1 = MG_CLAY1.value;
    let MG2 = MG_CLAY2.value;
    let MG3 = MG_CLAY3.value;

    if (P1 + P2 + P3 !== 100) {
        alert("Percentage must be 100");
        return;
    }

    let result = "";
    if (MG1) result += MG1 + "(" + P1 + "%)";
    if (MG2) result += (result ? "+" : "") + MG2 + "(" + P2 + "%)";
    if (MG3) result += (result ? "+" : "") + MG3 + "(" + P3 + "%)";

    if (!activeMgClayInput) {
        alert("No row selected");
        return;
    }

    activeMgClayInput.value = result;

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}

/* ================= INIT ================= */
Display_Mudgun_Details();
</script>
