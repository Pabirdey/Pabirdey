<!DOCTYPE html>
<html>
<head>
    <title>Production Summary</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 5px;
        }

        .container-fluid {
            padding: 0;
            max-width: 900px;
            margin: auto;
        }

        .production-box {
            border: 1px solid #000;
        }

        .production-title {
            text-align: center;
            font-size: 14px;
            font-weight: bold;
            padding: 3px;
            border-bottom: 1px solid #000;
        }

        .production-table {
            margin-bottom: 0;
        }

        .production-table th {
            text-align: center;
            vertical-align: middle;
            font-size: 11px;
            font-weight: bold;
            padding: 2px;
            background-color: #f5f5f5;
        }

        .production-table td {
            text-align: center;
            vertical-align: middle;
            padding: 1px;
        }

        .prod-input {
            width: 100%;
            height: 20px;
            border: 1px solid #3c5f7d;
            text-align: center;
            font-size: 11px;
            font-weight: bold;
            padding: 0;
        }

        .row-title {
            width: 40px;
            font-size: 11px;
            font-weight: bold;
            color: #003366;
        }

        .tot-color {
            color: #7c3aed;
            font-weight: bold;
            font-size: 11px;
        }

        .exp-color {
            color: #000;
            font-weight: bold;
            font-size: 11px;
        }

        .summary-row {
            color: brown;
            font-weight: bold;
            font-size: 11px;
            background-color: #fafafa;
        }
    </style>
</head>
<body>

<div class="container-fluid">

    <div class="production-box">

        <div class="production-title">
            On Date Production Summary
        </div>

        <table class="table table-bordered production-table">

            <thead>
                <tr>
                    <th></th>
                    <th>LD1</th>
                    <th>LD2</th>
                    <th>LD3</th>
                    <th>Granshot</th>
                    <th>MRD</th>
                    <th>TOT</th>
                    <th>Exp Prod</th>
                </tr>
            </thead>

            <tbody>

                <!-- C -->
                <tr>
                    <td class="row-title">C</td>
                    <td><input class="prod-input" value="397"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="450.15"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">1214.4</td>
                    <td class="exp-color">1943.0</td>
                </tr>

                <!-- E -->
                <tr>
                    <td class="row-title">E</td>
                    <td><input class="prod-input" value="459.98"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">564.9</td>
                    <td class="exp-color">903.9</td>
                </tr>

                <!-- F -->
                <tr>
                    <td class="row-title">F</td>
                    <td><input class="prod-input" value="2166.01"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="344.4"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">2611.2</td>
                    <td class="exp-color">4177.9</td>
                </tr>

                <!-- Total A-F -->
                <tr class="summary-row">
                    <td>TotA-F</td>
                    <td>3022.99</td>
                    <td>0</td>
                    <td>450.15</td>
                    <td>344.4</td>
                    <td>0</td>
                    <td>4390.5</td>
                    <td>7024.8</td>
                </tr>

                <!-- G -->
                <tr>
                    <td class="row-title">G</td>
                    <td><input class="prod-input" value="239"></td>
                    <td><input class="prod-input" value="2758.14"></td>
                    <td><input class="prod-input" value="946.7"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">4049.3</td>
                    <td class="exp-color">6478.9</td>
                </tr>

                <!-- H -->
                <tr>
                    <td class="row-title">H</td>
                    <td><input class="prod-input" value="244.3"></td>
                    <td><input class="prod-input" value="3465.35"></td>
                    <td><input class="prod-input" value="1750"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">5459.7</td>
                    <td class="exp-color">8735.4</td>
                </tr>

                <!-- I -->
                <tr>
                    <td class="row-title">I</td>
                    <td><input class="prod-input" value="2703.1"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="2066.76"></td>
                    <td><input class="prod-input" value="744.2"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td class="tot-color">5751.5</td>
                    <td class="exp-color">9202.4</td>
                </tr>

                <!-- Total A-I -->
                <tr class="summary-row">
                    <td>TotA-I</td>
                    <td>6209.39</td>
                    <td>6223.49</td>
                    <td>6213.61</td>
                    <td>1088.6</td>
                    <td>0</td>
                    <td>18669.3</td>
                    <td>31441.5</td>
                </tr>

            </tbody>

        </table>

    </div>

</div>

</body>
</html>
