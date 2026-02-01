/* ---------- DROPDOWN ---------- */
function showDropdown(btn) {
    $('.mgClayList').hide();
    $(btn).next('.mgClayList').show();
}

function selectClay(item, rowIndex) {

    let list = item.parentElement;
    let input = list.previousElementSibling;

    if (item.innerText === "OTHERS") {
        $("#hdnRowIndex").val(rowIndex);
        new bootstrap.Modal(document.getElementById("mgClayOtherModal")).show();
    } else {
        input.value = item.innerText;
    }

    list.style.display = "none";
}

/* ---------- MODAL SAVE ---------- */
function checkClay() {

    let p1 = Number(P1.value) || 0;
    let p2 = Number(P2.value) || 0;
    let p3 = Number(P3.value) || 0;

    if (p1 + p2 + p3 !== 100) {
        alert("Percentage must be 100");
        return;
    }

    let result = "";
    if (MG_CLAY1.value) result += MG_CLAY1.value + "(" + p1 + "%)";
    if (MG_CLAY2.value) result += (result ? "+" : "") + MG_CLAY2.value + "(" + p2 + "%)";
    if (MG_CLAY3.value) result += (result ? "+" : "") + MG_CLAY3.value + "(" + p3 + "%)";

    let rowIndex = $("#hdnRowIndex").val();
    let row = document.querySelectorAll("#Mudgun_Details tbody tr")[rowIndex];
    row.querySelector(".mgClayInput").value = result;

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}
