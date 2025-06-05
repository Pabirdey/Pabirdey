<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Solid Waste Entry</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .form-label {
            font-weight: bold;
            color: cyan;
            font-size: 14px;
        }
        .form-control, .form-select {
            height: 30px;
            font-size: 13px;
        }
        .highlight-box {
            background-color: yellow;
            font-weight: bold;
        }
        .ok-button {
            background-color: purple;
            color: white;
            border: none;
            padding: 5px 10px;
            margin-top: 30px;
        }
        .section {
            border-top: 2px solid #ccc;
            margin-top: 20px;
            padding-top: 10px;
        }
    </style>
</head>
<body class="p-3">

    <div class="container-fluid">
        <div class="row">
            <!-- Column 1 -->
            <div class="col-md-2">
                <label class="form-label">MIXED FLUX</label>
                <input type="text" class="form-control" value="14281">
                <label class="form-label">MILL SLUDGE</label>
                <input type="text" class="form-control" value="0">
                <label class="form-label">GCP SLUDGE</label>
                <input type="text" class="form-control" value="437.4">
                <label class="form-label">WRP</label>
                <input type="text" class="form-control" value="0">
                <label class="form-label">REVERT MATERIAL</label>
                <input type="text" class="form-control" value="4860">
            </div>

            <!-- Column 2 -->
            <div class="col-md-2">
                <label class="form-label">LD SLUDGE</label>
                <input type="text" class="form-control" value="1944">
                <label class="form-label">FLUE DUST</label>
                <input type="text" class="form-control" value="437.4">
                <label class="form-label">LD SLUDGE FRESH</label>
                <input type="text" class="form-control" value="1944">
                <label class="form-label">DOLO FINES</label>
                <input type="text" class="form-control">
                <label class="form-label">LD SLUDGE MIX</label>
                <input type="text" class="form-control">
            </div>

            <!-- Column 3 -->
            <div class="col-md-2">
                <label class="form-label">MILL SCALE</label>
                <input type="text" class="form-control" value="1117.8">
                <label class="form-label">ESP DUST</label>
                <input type="text" class="form-control" value="437.4">
                <label class="form-label">Lime Fines</label>
                <input type="text" class="form-control">
                <label class="form-label">FLUE DUST</label>
                <input type="text" class="form-control" value="437.4">
                <label class="form-label">SOLID MIX</label>
                <input type="text" class="form-control">
            </div>

            <!-- Column 4 -->
            <div class="col-md-2">
                <label class="form-label">KILN DUST</label>
                <input type="text" class="form-control" value="0">
                <label class="form-label">LD SLAG FINES</label>
                <input type="text" class="form-control" value="0">
                <label class="form-label">MILL SLUDGE</label>
                <input type="text" class="form-control" value="0">
                <label class="form-label">MILL SCALE</label>
                <input type="text" class="form-control" value="1117.8">
            </div>

            <!-- Column 5 (Solid Waste) -->
            <div class="col-md-2">
                <label class="form-label">Solid Waste</label>
                <input type="text" class="form-control highlight-box" value="4860">
                <button class="ok-button">Ok</button>
            </div>

            <!-- Column 6 (PSW / Blend) -->
            <div class="col-md-2">
                <label class="form-label">PSW1</label>
                <input type="text" class="form-control" value="4860">
                <label class="form-label">PSW2</label>
                <input type="text" class="form-control">
                <label class="form-label">Blend - I</label>
                <select class="form-select">
                    <option selected>14</option>
                    <!-- Add more options if needed -->
                </select>
                <label class="form-label">Blend - II</label>
                <select class="form-select">
                    <option selected></option>
                    <!-- Add more options if needed -->
                </select>
            </div>
        </div>
    </div>

</body>
</html>