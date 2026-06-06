<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Scrollable Table</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
            font-family: Verdana;
            font-size: 12px;
            padding: 20px;
        }

        /* Scrollable Table Container */
        .table-container {
            max-height: 240px; /* Height of 8 rows approximately */
            overflow-y: auto;
            overflow-x: auto;
            border: 1px solid #ccc;
        }

        .table {
            margin-bottom: 0;
            white-space: nowrap;
        }

        .table th {
            background: #1565c0;
            color: white;
            font-size: 14px;
            padding: 5px;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .table td {
            background: white;
            color: black;
            font-size: 14px;
            padding: 5px;
        }
    </style>
</head>
<body>

    <div class="container-fluid">

        <div class="table-container">
            <table class="table table-bordered text-center">
                <thead>
                    <tr>
                        <th>CastNo</th>
                        <th>Start</th>
                        <th>End</th>
                        <th>Ladle No</th>
                        <th>Start</th>
                        <th>End</th>
                        <th>Arrived From</th>
                        <th>Gross</th>
                        <th>Tare</th>
                        <th>Net</th>
                        <th>Pouring Rate</th>
                        <th>HMT</th>
                        <th>Reason For Outage</th>
                        <th>Seq_No</th>
                        <th>Delete</th>
                    </tr>
                </thead>

                <tbody id="tblBody">
                    <tr>
                        <td>1</td><td>08:00</td><td>08:10</td><td>L1</td>
                        <td>08:11</td><td>08:20</td><td>BF-1</td>
                        <td>100</td><td>20</td><td>80</td>
                        <td>10</td><td>HMT1</td><td>-</td><td>1</td><td>X</td>
                    </tr>

                    <tr>
                        <td>2</td><td>08:20</td><td>08:30</td><td>L2</td>
                        <td>08:31</td><td>08:40</td><td>BF-2</td>
                        <td>110</td><td>22</td><td>88</td>
                        <td>11</td><td>HMT2</td><td>-</td><td>2</td><td>X</td>
                    </tr>

                    <tr><td>3</td><td colspan="14">Data Row 3</td></tr>
                    <tr><td>4</td><td colspan="14">Data Row 4</td></tr>
                    <tr><td>5</td><td colspan="14">Data Row 5</td></tr>
                    <tr><td>6</td><td colspan="14">Data Row 6</td></tr>
                    <tr><td>7</td><td colspan="14">Data Row 7</td></tr>
                    <tr><td>8</td><td colspan="14">Data Row 8</td></tr>
                    <tr><td>9</td><td colspan="14">Data Row 9</td></tr>
                    <tr><td>10</td><td colspan="14">Data Row 10</td></tr>
                    <tr><td>11</td><td colspan="14">Data Row 11</td></tr>
                    <tr><td>12</td><td colspan="14">Data Row 12</td></tr>
                    <tr><td>13</td><td colspan="14">Data Row 13</td></tr>
                    <tr><td>14</td><td colspan="14">Data Row 14</td></tr>
                    <tr><td>15</td><td colspan="14">Data Row 15</td></tr>
                </tbody>
            </table>
        </div>

    </div>

</body>
</html>
