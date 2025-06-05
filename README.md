<!DOCTYPE html>
<html>
<head>
    <title>Textbox Sum</title>
</head>
<body>
    <label>Number 1:</label>
    <input type="number" id="num1" onblur="calculateSum()" /><br><br>

    <label>Number 2:</label>
    <input type="number" id="num2" onblur="calculateSum()" /><br><br>

    <label>Sum:</label>
    <input type="text" id="sum" readonly />

    <script>
        function calculateSum() {
            var n1 = parseFloat(document.getElementById("num1").value) || 0;
            var n2 = parseFloat(document.getElementById("num2").value) || 0;
            var total = n1 + n2;
            document.getElementById("sum").value = total;
        }
    </script>
</body>
</html>