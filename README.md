<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Quantity</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .form-label {
            font-weight: 500;
        }
        .section-divider {
            border-top: 2px solid #bbb;
            margin-top: 10px;
            margin-bottom: 20px;
        }
        .material-label {
            text-align: right;
            padding-top: calc(0.375rem + 1px); /* align with input */
        }
    </style>
</head>
<body>
<div class="container mt-4">
    <h4 class="mb-4">Raw Material Quantity</h4>

    <!-- Header Form -->
    <form>
        <div class="row mb-3">
            <div class="col-md-2">
                <label class="form-label">PILE NO</label>
                <input type="text" class="form-control">
            </div>
            <div class="col-md-2">
                <label class="form-label">Source</label>
                <select class="form-select">
                    <option>RMBB</option>
                </select>
            </div>
            <div class="col-md-1">
                <label class="form-label">Shift</label>
                <select class="form-select">
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                </select>
            </div>
            <div class="col-md-2">
                <label class="form-label">Start Date</label>
                <input type="date" class="form-control">
            </div>
            <div class="col-md-1">
                <label class="form-label">Hr.</label>
                <input type="number" class="form-control" min="0" max="23">
            </div>
            <div class="col-md-1">
                <label class="form-label">Mi.</label>
                <input type="number" class="form-control" min="0" max="59">
            </div>
            <div class="col-md-2">
                <label class="form-label">End Date</label>
                <input type="date" class="form-control">
            </div>
            <div class="col-md-1">
                <label class="form-label">Hr.</label>
                <input type="number" class="form-control" min="0" max="23">
            </div>
            <div class="col-md-1">
                <label class="form-label">Mi.</label>
                <input type="number" class="form-control" min="0" max="59">
            </div>
        </div>

        <div class="row mb-3">
            <div class="col-md-2">
                <label class="form-label">Cons St. Date</label>
                <input type="date" class="form-control">
            </div>
            <div class="col-md-1">
                <label class="form-label">Hr.</label>
                <input type="number" class="form-control" min="0" max="23">
            </div>
            <div class="col-md-1">
                <label class="form-label">Mi.</label>
                <input type="number" class="form-control" min="0" max="59">
            </div>
        </div>

        <!-- Divider -->
        <hr class="section-divider">

        <!-- Material Rows -->
        <div class="row mb-2">
            <div class="col-md-2 material-label">NOA FINES</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">JODA FINES</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">YARD FINES</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
        </div>

        <div class="row mb-2">
            <div class="col-md-2 material-label">NOA Crushed</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">Joda Crushed</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">Pilbhara</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
        </div>

        <div class="row mb-2">
            <div class="col-md-2 material-label">Kirandul S/O (LUMP)</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">FSF VENEZUELAN</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">SN Feed Value</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
        </div>

        <!-- More material rows -->
        <div class="row mb-2">
            <div class="col-md-2 material-label">Bacheli</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">Jaroli</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">KAY PEE ENTP</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
        </div>

        <div class="row mb-4">
            <div class="col-md-2 material-label">AHLUWALIA FINES</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">Diatari</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
            <div class="col-md-2 material-label">Domestic IOF</div>
            <div class="col-md-2"><input class="form-control" type="text"></div>
        </div>

        <!-- Submit Button -->
        <button type="submit" class="btn btn-success">Save</button>
    </form>
</div>
</body>
</html>