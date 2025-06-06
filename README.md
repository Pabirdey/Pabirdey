<!DOCTYPE html>
<html>
<head>
    <title>Live Sum with Auto-Jump</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="p-4">
    <div class="container">
        <h4 class="mb-4">Live Sum of Two Numbers</h4>

        <div class="row mb-3">
            <div class="col-md-4">
                <label class="form-label">Number 1:</label>
                <input type="number" id="num1" class="form-control" oninput="calculateSum()" onkeydown="jumpToNext(event, 'num2')" />
            </div>

            <div class="col-md-4">
                <label class="form-label">Number 2:</label>
                <input type="number" id="num2" class="form-control" oninput="calculateSum()" onkeydown="jumpToNext(event, 'sum')" />
            </div>

            <div class="col-md-4">
                <label class="form-label">Sum:</label>
                <input type="text" id="sum" class="form-control" readonly />
            </div>
        </div>
    </div>

    <script>
        function calculateSum() {
            var n1 = parseFloat(document.getElementById("num1").value);
            var n2 = parseFloat(document.getElementById("num2").value);

            if (isNaN(n1)) n1 = 0;
            if (isNaN(n2)) n2 = 0;

            var total = n1 + n2;
            document.getElementById("sum").value = total.toFixed(2);
        }

        function jumpToNext(event, nextId) {
            if (event.key === "Enter") {
                event.preventDefault();
                document.getElementById(nextId).focus();
            }
        }
    </script>
</body>
</html>