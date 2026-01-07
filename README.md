<!DOCTYPE html>
<html>
<head>
    <title>Percentage Validation</title>
</head>

<body>

Percent 1 :
<input type="number" id="p1" value="0" oninput="checkPercent()">

<br><br>

Percent 2 :
<input type="number" id="p2" value="0" oninput="checkPercent()">

<br><br>

Percent 3 :
<input type="number" id="p3" value="0" oninput="checkPercent()">

<br><br>

Total :
<input type="text" id="totalTxt" readonly>

<br><br>

<span id="msg" style="font-weight:bold;color:red"></span>

<script>

function checkPercent() {

    var p1 = Number(document.getElementById("p1").value) || 0;
    var p2 = Number(document.getElementById("p2").value) || 0;
    var p3 = Number(document.getElementById("p3").value) || 0;

    var total = p1 + p2 + p3;

    document.getElementById("totalTxt").value = total;

    var msg = document.getElementById("msg");

    if (total == 100) {
        msg.style.color = "green";
        msg.innerText = "OK – Total is exactly 100%";
    }
    else if (total > 100) {
        msg.style.color = "red";
        msg.innerText = "Error – Percentage exceeded 100%";
    }
    else {
        msg.style.color = "blue";
        msg.innerText = "Remaining " + (100 - total) + "% needed";
    }
}

</script>

</body>
</html>