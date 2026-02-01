  function checkClay() {

    var P1 = Number(document.getElementById("P1").value) || 0;
    var P2 = Number(document.getElementById("P2").value) || 0;
    var P3 = Number(document.getElementById("P3").value) || 0;

    var MG1 = MG_CLAY1.value;
    var MG2 = MG_CLAY2.value;
    var MG3 = MG_CLAY3.value;

    var P_Sum = P1 + P2 + P3;

    if (P_Sum !== 100) {
        alert("Sum of Percentage is " + P_Sum + ". It should be 100.");
        return;
    }

    var result = "";

    if (MG1) result += MG1 + "(" + P1 + "%)";
    if (MG2) result += (result ? "+" : "") + MG2 + "(" + P2 + "%)";
    if (MG3) result += (result ? "+" : "") + MG3 + "(" + P3 + "%)";

    // ✅ GET ROW INDEX
    var rowIndex = Number(document.getElementById("hdnRowIndex").value);

    // ✅ GET ROW
    var row = document.querySelectorAll("#Mudgun_Details tbody tr")[rowIndex];

    if (!row) {
        console.error("Row not found");
        return;
    }

    // ✅ GET INPUT INSIDE THAT ROW
    var mgClayInput = row.querySelector(".mgClayInput");

    if (!mgClayInput) {
        console.error("mgClayInput not found");
        return;
    }

    // ✅ SET VALUE
    mgClayInput.value = result;

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}
