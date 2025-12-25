<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Entry</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body{
            background:#d1ffb0;
        }

        .form-panel{
            background:#2f8a2f;
            color:white;
            padding:20px;
            border-radius:8px;
            width:85%;
            margin:auto;
        }

        .heading-box{
            background:#1b4d1b;
            padding:10px;
            border-radius:8px;
            margin-bottom:15px;
        }

        .table-header{
            color:yellow;
            font-weight:bold;
            text-align:center;
        }

        .material-name{
            font-weight:bold;
            color:#ffe9e9;
        }

        input{
            text-align:right;
            font-weight:bold;
        }
    </style>
</head>
<body>

<div class="form-panel">

    <!-- Top Section -->
    <div class="heading-box d-flex justify-content-between align-items-center">
        <div>
            <label class="fw-bold">Date:</label>
            <input type="date" class="form-control d-inline-block" style="width:210px;">
        </div>

        <div>
            <label class="fw-bold">Furnace:</label>
            <select class="form-select d-inline-block" style="width:140px;">
                <option>A</option>
                <option>B</option>
                <option selected>C</option>
                <option>D</option>
            </select>
        </div>
    </div>

    <!-- Table -->
    <div class="row fw-bold table-header">
        <div class="col-4">RAW MATERIAL</div>
        <div class="col-3">Value in Tons</div>
        <div class="col-3">Value in Kgs</div>
        <div class="col-2">Types</div>
    </div>

    <hr>

    <!-- DATA ROWS -->
    <div id="rowsContainer">

        <!-- Example Row (Repeat for all items) -->
        <div class="row mb-2 align-items-center">
            <div class="col-4 material-name">COAL</div>

            <div class="col-3">
                <input class="form-control" value="0">
            </div>

            <div class="col-3">
                <input class="form-control" value="0">
            </div>

            <div class="col-2">
                <select class="form-select">
                    <option>IPC</option>
                    <option>Imported</option>
                    <option>Local</option>
                </select>
            </div>
        </div>

        <!-- Copy this row for EVERY ITEM in your list -->
        <div class="row mb-2 align-items-center">
            <div class="col-4 material-name">NUT COKE</div>
            <div class="col-3"><input class="form-control" value="161.460906"></div>
            <div class="col-3"><input class="form-control" value="161460.906"></div>
            <div class="col-2">
                <select class="form-select">
                    <option>BF Sized</option>
                    <option>Joda</option>
                </select>
            </div>
        </div>

        <div class="row mb-2 align-items-center">
            <div class="col-4 material-name">SINTER</div>
            <div class="col-3"><input class="form-control" value="1403.78925"></div>
            <div class="col-3"><input class="form-control" value="1403789.25"></div>
            <div class="col-2">
                <select class="form-select">
                    <option>Local</option>
                    <option>Imported</option>
                </select>
            </div>
        </div>

        <!-- Add all remaining items same way -->

    </div>

    <hr>

    <!-- Buttons -->
    <div class="text-center">
        <button class="btn btn-primary px-4">Save</button>
        <button class="btn btn-secondary px-4">Back</button>
    </div>

</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

</body>
</html>