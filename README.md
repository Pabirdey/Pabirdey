function checkClay() {
            var P1 = Number(document.getElementById("P1").value) || 0;
            var P2 = Number(document.getElementById("P2").value) || 0;
            var P3 = Number(document.getElementById("P3").value) || 0;
            var MG1 = MG_CLAY1.value;
            var MG2 = MG_CLAY2.value;
            var MG3 = MG_CLAY3.value;
            var P_Sum = P1 + P2 + P3;
            // -------- If NOT 100 ----------
            if (P_Sum !== 100) {
                alert("Sum of Percentage is " + P_Sum + ". It should be 100.");
                // MG_CLAY_USED.value = "Sum is " + P_Sum + "%. It should be 100%";
                return;
            }
            // -------- If 100 ----------
            var result = "";
            if (MG1 && !MG2 && !MG3)
                result = MG1 + "(" + P1 + "%)";
            if (MG1 && MG2 && !MG3)
                result = MG1 + "(" + P1 + "%)+" + MG2 + "(" + P2 + "%)";
            if (MG1 && MG2 && MG3)
                result = MG1 + "(" + P1 + "%)+" + MG2 + "(" + P2 + "%)+" + MG3 + "(" + P3 + "%)";
            if (!MG1 && MG2 && !MG3)
                result = MG2 + "(" + P2 + "%)";
            if (!MG1 && MG2 && MG3)
                result = MG2 + "(" + P2 + "%)+" + MG3 + "(" + P3 + "%)";
            if (!MG1 && !MG2 && MG3)
                result = MG3 + "(" + P3 + "%)";
            if (MG1 && !MG2 && MG3)
                result = MG1 + "(" + P1 + "%)+" + MG3 + "(" + P3 + "%)";
            if (!MG1 && !MG2 && !MG3)
                result = "";
            mgClayInput.value = result;
        }
