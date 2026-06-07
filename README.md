<!DOCTYPE html>
<html>
<head>
    <title>Production Summary</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>

        .production-box {
            border: 2px solid #000;
            margin-top: 20px;
        }

        .production-title {
            text-align: center;
            font-size: 32px;
            font-weight: bold;
            padding: 10px;
            border-bottom: 2px solid #000;
        }

        .production-table {
            margin-bottom: 0;
        }

        .production-table th {
            text-align: center;
            vertical-align: middle;
            font-size: 24px;
            font-weight: bold;
        }

        .production-table td {
            text-align: center;
            vertical-align: middle;
        }

        .prod-input {
            width: 100%;
            border: 2px solid #3c5f7d;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
            background: #fff;
            height: 50px;
        }

        .tot-color {
            color: #7c3aed;
            font-weight: bold;
            font-size: 26px;
        }

        .exp-color {
            color: #000;
            font-weight: bold;
            font-size: 26px;
        }

        .summary-row {
            color: brown;
            font-weight: bold;
            font-size: 24px;
        }

        .row-title {
            font-size: 28px;
            font-weight: bold;
            color: #003366;
            width: 100px;
        }

    </style>

</head>
<body>

<div class="container-fluid">

    <div class="production-box">

        <div class="production-title">
            On Date Production Summary :
        </div>

        <table class="table table-bordered production-table">

            <thead>

                <tr>
                    <th style="width:100px;"></th>
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

                <tr>
                    <td class="row-title">A</td>

                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>

                    <td class="tot-color">0</td>
                    <td class="exp-color">0</td>
                </tr>

                <tr>
                    <td class="row-title">B</td>

                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>

                    <td class="tot-color">0</td>
                    <td class="exp-color">0</td>
                </tr>

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

                <tr>
                    <td class="row-title">D</td>

                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>
                    <td><input class="prod-input" value="0"></td>

                    <td class="tot-color">0</td>
                    <td class="exp-color">0</td>
                </tr>

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