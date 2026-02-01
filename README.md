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

    let rowIndex = Number($("#hdnRowIndex").val());
    let rows = document.querySelectorAll("#Mudgun_Details tbody tr");

    if (!rows[rowIndex]) {
        console.error("Row not found at index:", rowIndex);
        return;
    }

    let input = rows[rowIndex].querySelector(".mgClayInput");

    if (!input) {
        console.error("mgClayInput not found in row:", rowIndex);
        return;
    }

    input.value = result;

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}
