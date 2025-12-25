<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Entry</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body{
            background:#d6ffd6;
        }
        .panel-box{
            background:#2e8b57;
            color:white;
            padding:15px;
            border-radius:8px;
            margin-bottom:20px;
        }
        .inner-panel{
            background:#3fa35c;
            padding:15px;
            border-radius:8px;
        }
        .label-col{
            color:#fff;
            font-weight:600;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-4">

    <!-- Top Filter -->
    <div class="panel-box">
        <div class="row align-items-center">
            <div class="col-md-4">
                <label class="form-label">Date:</label>
                <input type="date" class="form-control">
            </div>

            <div class="col-md-4">
                <label class="form-label">Furnace:</label>
                <select class="form-select">
                    <option>F</option>
                    <option>E</option>
                </select>
            </div>
        </div>
    </div>

    <!-- Main Panel -->
    <div class="panel-box">
        <div class="inner-panel">

            <div class="row fw-bold text-warning mb-2">
                <div class="col-md-3">Material</div>
                <div class="col-md-3">Value in Tons</div>
                <div class="col-md-3">Value in Kgs</div>
                <div class="col-md-3">Types</div>
            </div>

            <!-- === ROW 1 === -->
            <div class="row mb-2">
                <div class="col-md-3 label-col">COAL</div>
                <div class="col-md-3"><input class="form-control" /></div>
                <div class="col-md-3"><input class="form-control" /></div>
                <div class="col-md-3">
                    <select class="form-select">
                        <option>IPC</option>
                        <option>ABC</option>
                    </select>
                </div>
            </div>

            <!-- === ROW 2 === -->
            <div class="row mb-2">
                <div class="col-md-3 label-col">NUT COKE</div>
                <div class="col-md-3"><input class="form-control" /></div>
                <div class="col-md-3"><input class="form-control" /></div>
                <div class="col-md-3">
                    <select class="form-select">
                        <option>BF SIZED JODA</option>
                    </select>
                </div>
            </div>

            <!-- Repeat same structure for all other materials -->

            <!-- Theoretical Production -->
            <div class="row mt-4">
                <div class="col-md-4 label-col">Theoretical Production</div>
                <div class="col-md-4">
                    <input class="form-control" readonly value="4307.16">
                </div>
            </div>

            <!-- Buttons -->
            <div class="mt-4">
                <button class="btn btn-primary">Save</button>
                <button class="btn btn-secondary ms-2">Back</button>
            </div>

        </div>
    </div>

</div>

</body>
</html>