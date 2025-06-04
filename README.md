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
            margin-left:2px;
        }

        .material-label {
            text-align: left;
            padding-top: calc(0.375rem + 1px); 
        }
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4">Raw Material Quantity</h4>        
        <form>
            @*<div class="row mb-3">
                <div class="col-md-2">
                    <label class="form-label">PILE NO</label>
                    <input type="text" class="form-control">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Source</label>
                    <select class="form-select">
                        <option>RMBB_KNR</option>
                        <option>RMBB</option>
                        <option>RMBBN</option>
                    </select>
                </div>
                <div class="col-md-1">
                    <label class="form-label">Shift</label>
                    <select class="form-select">
                        <option>A</option>
                        <option>B</option>
                        <option>C</option>
                    </select>
                </div>
                <div class="col-md-2">
                    <label class="form-label">Start Date</label>
                    <input type="date" class="form-control">
                </div>               
            </div>*@           
            
            <hr class="section-divider">            
            <div class="row mb-2">
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">NOA FINES</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">JODA FINES</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">KB FINES</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">YARD FINES</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">BHJ</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">Namisa</label>
                    <input class="form-control w-50" type="text">
                </div>
               
            </div>
            <div class="row mb-2">
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">Fortescue BF</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">Noa Crushed</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-3 mb-0">Joda Crushed</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">KB Crushed</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-4 mb-0">Pilbhara</label>
                    <input class="form-control w-50" type="text">
                </div>
                <div class="col-md-2 d-flex align-items-center">
                    <label class="me-5 mb-0">Kumba</label>
                    <input class="form-control w-50" type="text">
                </div>               

            </div>
           
        </form>
    </div>
</body>
</html>
