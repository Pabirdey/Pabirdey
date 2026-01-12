<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Bootstrap + jQuery Date Picker</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        body {
            font-family: Courier New, Courier, monospace;
            background: #f4f6f9;
        }

        .card-box {
            width: 420px;
            margin: 80px auto;
            padding: 25px;
            background: #ffffff;
            border-radius: 15px;
            box-shadow: 0 0 18px rgba(0,0,0,0.15);
        }

        label {
            font-size: 18px;
            font-weight: bold;
        }
    </style>
</head>

<body>

<div class="card-box">

    <!-- DATE -->
    <div class="mb-3">
        <label>Select Date</label>
        <input type="date"
               id="tbFDatePick"
               class="form-control text-center">
    </div>

    <!-- DATE TIME -->
    <div class="mb-3">
        <label>Select Date & Time</label>
        <input type="datetime-local"
               id="tbFDateTime"
               class="form-control text-center">
    </div>

    <div class="text-center">
        <button class="btn btn-primary" id="btnShow">
            Show Values
        </button>
    </div>

</div>

<script>
    let selectedDate = "";
    let selectedDateTime = "";

    $(document).ready(function () {

        // Date change
        $("#tbFDatePick").on("change", function () {
            selectedDate = $(this).val();   // yyyy-mm-dd
            console.log("Date:", selectedDate);
        });

        // DateTime change
        $("#tbFDateTime").on("change", function () {
            selectedDateTime = $(this).val(); // yyyy-mm-ddTHH:mm
            console.log("DateTime:", selectedDateTime);
        });

        // Button click
        $("#btnShow").on("click", function () {
            alert(
                "Selected Date : " + selectedDate +
                "\nSelected DateTime : " + selectedDateTime
            );
        });

    });
</script>

</body>
</html>
