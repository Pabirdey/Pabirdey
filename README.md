<!DOCTYPE html>
<html>
<head>

    <title>Production Breakup</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
          rel="stylesheet" />

    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <style>

        body {
            background: #f4f7fb;
        }

        .main-box {
            background: linear-gradient(to bottom,#003399,#00bfff);
            padding: 20px;
            border-radius: 12px;
            margin-top: 30px;
        }

        .title {
            color: white;
            text-align: center;
            font-size: 32px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        table {
            background: white;
        }

        th {
            background: #003399 !important;
            color: white !important;
            vertical-align: middle;
        }

        td {
            vertical-align: middle;
        }

        .reportedOnDate {
            text-align: center;
            font-weight: bold;
        }

        .reportedToDate,
        .balance {
            font-weight: bold;
        }

        .balance-negative {
            color: red;
        }

        .balance-positive {
            color: green;
        }

    </style>

</head>

<body>

    <div class="container">

        <div class="main-box">

            <div class="title">
                Production Breakup
            </div>

            <table class="table table-bordered text-center">

                <thead>
                    <tr>
                        <th>Furnace</th>
                        <th>Actual OnDate</th>
                        <th>Actual ToDate</th>
                        <th>Reported OnDate</th>
                        <th>Reported ToDate</th>
                        <th>Balance</th>
                    </tr>
                </thead>

                <tbody>

                    <!-- Row 1 -->
                    <tr>

                        <td><b>C</b></td>

                        <td>1698</td>

                        <td class="actualToDate">
                            5792
                        </td>

                        <td>
                            <input type="number"
                                   class="form-control reportedOnDate"
                                   value="0" />
                        </td>

                        <td class="reportedToDate"
                            data-old="5600">
                            5600
                        </td>

                        <td class="balance balance-positive"
                            data-old="192">
                            192
                        </td>

                    </tr>


                    <!-- Row 2 -->
                    <tr>

                        <td><b>E</b></td>

                        <td>1220</td>

                        <td class="actualToDate">
                            19698
                        </td>

                        <td>
                            <input type="number"
                                   class="form-control reportedOnDate"
                                   value="0" />
                        </td>

                        <td class="reportedToDate"
                            data-old="19700">
                            19700
                        </td>

                        <td class="balance balance-negative"
                            data-old="-2">
                            -2
                        </td>

                    </tr>

                </tbody>

            </table>

        </div>

    </div>


    <script>

        $(document).on("input", ".reportedOnDate", function () {

            let row = $(this).closest("tr");

            // User entered value
            let enteredValue =
                parseFloat($(this).val()) || 0;

            // Original Reported ToDate
            let originalReportedToDate =
                parseFloat(
                    row.find(".reportedToDate").attr("data-old")
                ) || 0;

            // Original Balance
            let originalBalance =
                parseFloat(
                    row.find(".balance").attr("data-old")
                ) || 0;

            // Add entered value to Reported ToDate
            let newReportedToDate =
                originalReportedToDate + enteredValue;

            // Subtract entered value from Balance
            let newBalance =
                originalBalance - enteredValue;

            // Set new Reported ToDate
            row.find(".reportedToDate")
                .text(newReportedToDate);

            // Set new Balance
            row.find(".balance")
                .text(newBalance);

            // Balance color change
            row.find(".balance")
                .removeClass("balance-positive balance-negative");

            if (newBalance < 0) {
                row.find(".balance")
                    .addClass("balance-negative");
            }
            else {
                row.find(".balance")
                    .addClass("balance-positive");
            }

        });

    </script>

</body>
</html>