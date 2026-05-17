<!DOCTYPE html>
<html>
<head>

    <title>Production Breakup</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
          rel="stylesheet" />

    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

</head>

<body>

<div class="container mt-4">

    <table class="table table-bordered text-center">

        <thead>
            <tr>
                <th>Furnace</th>
                <th>Reported OnDate</th>
                <th>Reported ToDate</th>
                <th>Balance</th>
            </tr>
        </thead>

        <tbody>

            <tr>
                <td>C</td>

                <td>
                    <input type="text" id="REPORTED_C" value="100" class="form-control">
                </td>

                <td>
                    <input type="text" id="REPORTED_C_TD" value="5600" class="form-control" readonly>
                </td>

                <td>
                    <input type="text" id="BALANCE_C" value="192" class="form-control" readonly>
                </td>
            </tr>

        </tbody>

    </table>

</div>


<script>

    // store original values in JS (EASY METHOD)
    let oldValue = {};

    $(document).ready(function () {

        oldValue["C"] = parseFloat($("#REPORTED_C").val()) || 0;

    });


    $("#REPORTED_C").keydown(function (e) {

        if (e.keyCode == 9) {

            let newVal = parseFloat($("#REPORTED_C").val()) || 0;

            let diff = newVal - oldValue["C"];

            // update ToDate
            let toDate = parseFloat($("#REPORTED_C_TD").val()) || 0;
            $("#REPORTED_C_TD").val(Math.round(toDate + diff));

            // update Balance
            let bal = parseFloat($("#BALANCE_C").val()) || 0;
            $("#BALANCE_C").val(Math.round(bal - diff));

            // update memory
            oldValue["C"] = newVal;
        }
    });

</script>

</body>
</html>
