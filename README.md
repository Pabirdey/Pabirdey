<!DOCTYPE html>
<html>
<head>
    <title>Live Sum</title>
</head>
<body>
    <label>Number 1:</label>
    <input type="number" id="num1" oninput="calculateSum()" /><br><br>

    <label>Number 2:</label>
    <input type="number" id="num2" oninput="calculateSum()" /><br><br>

    <label>Sum:</label>
    <input type="text" id="sum" readonly />

    <script>
        function calculateSum() {
            var n1 = parseFloat(document.getElementById("num1").value);
            var n2 = parseFloat(document.getElementById("num2").value);

            if (isNaN(n1) || isNaN(n2)) {
                document.getElementById("sum").value = "";
                return;
            }

            var total = n1 + n2;
            document.getElementById("sum").value = total.toFixed(2); // 2 decimal places
        }
    </script>
</body>
</html>