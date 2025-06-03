@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}

<!DOCTYPE html>
<html>
<head>
    <title>Bootstrap 5 Layout Horizontal form</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
          rel="stylesheet"
          integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
          crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"
            integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM"
            crossorigin="anonymous">
    </script>
</head>

<body>
    <form class="container-fluid mt-4">
        <h3 class="text-success mb-4">Raw Material Quantity</h3>
        <div class="row g-3 align-items-center">

            <div class="col-md-2 d-flex align-items-center">
                <label for="pileNo" class="me-2">Pile No:</label>
                <input type="text" class="form-control" id="pileNo" placeholder="Pile No">
            </div>

            <div class="col-md-2 d-flex align-items-center">
                <label for="source" class="me-2">Source:</label>
                <select class="form-select" id="source" style="width: 130px;">
                    <option value="RMBB_KNR">RMBB_KNR</option>
                    <option value="RMBB">RMBB</option>
                    <option value="RMBBN">RMBBN</option>
                </select>
            </div>

            <div class="col-md-2 d-flex align-items-center">
                <label for="shift" class="me-2">Shift:</label>
                <select class="form-select" id="shift" style="width: 80px;">
                    <option value="A">A</option>
                    <option value="B">B</option>
                    <option value="C">C</option>
                </select>
            </div>

            <div class="col-md-3 d-flex align-items-center">
                <label for="startDate" class="me-2">Start Date:</label>
                <input type="date" class="form-control" id="startDate">
            </div>

            <div class="col-md-3 d-flex align-items-center">
                <label for="endDate" class="me-2">End Date:</label>
                <input type="date" class="form-control" id="endDate">
            </div>

            <div class="col-md-3 d-flex align-items-center">
                <label for="consStDate" class="me-2">Cons. St. Date:</label>
                <input type="date" class="form-control" id="consStDate">
            </div>

        </div>
    </form>
</body>
</html>
