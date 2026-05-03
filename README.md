<!DOCTYPE html>
<html>
<head>
    <title>Coke Unloading</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f4f4;
            padding: 20px;
        }

        .card-box {
            background: #0d6efd;
            padding: 15px;
            border-radius: 12px;
            color: white;
            margin-bottom: 20px;
        }

        .table th, .table td {
            text-align: center;
            vertical-align: middle;
        }

        .table input {
            width: 70px;
            text-align: center;
        }

        .title {
            font-weight: bold;
            text-align: center;
            margin-bottom: 10px;
            font-size: 18px;
        }

        .sign-box {
            background: #0d6efd;
            padding: 10px;
            border-radius: 10px;
            color: white;
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .sign-box select {
            width: 200px;
        }
    </style>
</head>

<body>

<div class="container-fluid">

    <div class="row">

        <!-- 🔵 Coke Table -->
        <div class="col-md-6">
            <div class="card-box">
                <div class="title">Tonnage of Coke</div>

                <table class="table table-bordered bg-white text-dark">
                    <thead>
                        <tr>
                            <th>Bunker</th>
                            <th>A</th>
                            <th>B</th>
                            <th>C</th>
                            <th>D</th>
                            <th>E</th>
                            <th>F</th>
                            <th>Total</th>
                        </tr>
                    </thead>
                    <tbody>

                        <!-- ROW -->
                        <tr>
                            <td>WESTERN</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                        <tr>
                            <td>MIDDLE</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                        <tr>
                            <td>EASTERN</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                        <tr>
                            <td>ST_COKE</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                    </tbody>
                </table>
            </div>
        </div>

        <!-- 🔵 Nut Coke Table -->
        <div class="col-md-6">
            <div class="card-box">
                <div class="title">Tonnage of Nut Coke</div>

                <table class="table table-bordered bg-white text-dark">
                    <thead>
                        <tr>
                            <th>Bunker</th>
                            <th>A</th>
                            <th>B</th>
                            <th>C</th>
                            <th>D</th>
                            <th>E</th>
                            <th>F</th>
                            <th>Total</th>
                        </tr>
                    </thead>
                    <tbody>

                        <tr>
                            <td>WEST</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                        <tr>
                            <td>MID</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                        <tr>
                            <td>EAST</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>

                    </tbody>
                </table>
            </div>
        </div>

    </div>

    <!-- 🔵 Sign Off Section -->
    <div class="sign-box mt-3">
        <select class="form-select">
            <option>Select Name</option>
            <option>Operator 1</option>
            <option>Operator 2</option>
        </select>

        <div>
            <input type="checkbox"> Sign OFF
        </div>
    </div>

</div>

</body>
</html>