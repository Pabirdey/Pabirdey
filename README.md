<!DOCTYPE html>
<html>
<head>
<title>Clay Percentage Validation</title>
</head>

<body>

<h3>Clay Details</h3>

Clay 1 :
<select id="MG_CLAY1">
  <option value=""></option>
  <option>ACE</option>
  <option>BRL</option>
  <option>HARIMA</option>
</select>
<input id="P1" placeholder="%">

<br><br>

Clay 2 :
<select id="MG_CLAY2">
  <option value=""></option>
  <option>ACE</option>
  <option>BRL</option>
  <option>HARIMA</option>
</select>
<input id="P2" placeholder="%">

<br><br>

Clay 3 :
<select id="MG_CLAY3">
  <option value=""></option>
  <option>ACE</option>
  <option>BRL</option>
  <option>HARIMA</option>
</select>
<input id="P3" placeholder="%">

<br><br>

Result :
<input id="MG_CLAY_USED" readonly style="width:350px">

<br><br>

<button onclick="checkClay()">Save</button>


<script>

function checkClay() {

    var P1 = Number(P1.value) || 0;
    var P2 = Number(P2.value) || 0;
    var P3 = Number(P3.value) || 0;

    var MG1 = MG_CLAY1.value;
    var MG2 = MG_CLAY2.value;
    var MG3 = MG_CLAY3.value;

    var P_Sum = P1 + P2 + P3;

    // -------- If NOT 100 ----------
    if (P_Sum !== 100) {
        alert("Sum of Percentage is " + P_Sum + ". It should be 100.");
        alert("Sum of Percentage is " + P_Sum + ". It should be 100.");

        MG_CLAY_USED.value = "Sum is " + P_Sum + "%. It should be 100%";
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

    MG_CLAY_USED.value = result;
}

</script>

</body>
</html>