@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}

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

        .material-row .form-label {
            padding-top: 0.375rem;
        }

        .material-row .col-md-2 {
            display: flex;
            align-items: center;
        }

        .material-row .form-control {
            flex: 1;
        }

        .material-row label {
            min-width: 100px;
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4">Raw Material Quantity</h4>        
        <form>
            <hr class="section-divider">

            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">NOA FINES</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">JODA FINES</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB FINES</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">YARD FINES</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text">
                </div>
            </div>

            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text">
                </div>
            </div>
        </form>
    </div>
</body>
</html>