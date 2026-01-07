<!DOCTYPE html>
<html>
<head>
<title>Clay Validation</title>
</head>

<body>

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
<input id="MG_CLAY_USED" readonly style="width:300px">

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

    var sum = P1 + P2 + P3;

    if (sum !== 100) {
        alert("Sum is " + sum + "%. It must be 100%");
        return;
    }

    var result = "";

    if (MG1) result = MG1 + "(" + P1 + "%)";
    if (MG2) {
        if (result !== "") result += "+";
        result += MG2 + "(" + P2 + "%)";
    }
    if (MG3) {
        if (result !== "") result += "+";
        result += MG3 + "(" + P3 + "%)";
    }

    MG_CLAY_USED.value = result;
}

</script>

</body>
</html>