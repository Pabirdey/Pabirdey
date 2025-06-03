@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>Bootstrap 5 Horizontal Form</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
          rel="stylesheet"
          crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"
            crossorigin="anonymous"></script>
</head>
<body>
    <form class="container mt-4">
        <h3 class="text-success mb-4">Raw Material Quantity</h3>

        <div class="row gy-3">

            <!-- Pile No -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="pileNo" class="form-label me-2 mb-0" style="min-width: 80px;">Pile No:</label>
                <input type="text" class="form-control" id="pileNo" placeholder="Pile No">
            </div>

            <!-- Source -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="source" class="form-label me-2 mb-0" style="min-width: 60px;">Source:</label>
                <select class="form-select" id="source" style="width: 130px;">
                    <option value="RMBB_KNR">RMBB_KNR</option>
                    <option value="RMBB">RMBB</option>
                    <option value="RMBBN">RMBBN</option>
                </select>
            </div>

            <!-- Shift -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="shift" class="form-label me-2 mb-0" style="min-width: 50px;">Shift:</label>
                <select class="form-select" id="shift" style="width: 80px;">
                    <option value="A">A</option>
                    <option value="B">B</option>
                    <option value="C">C</option>
                </select>
            </div>

            <!-- Start Date -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="startDate" class="form-label me-2 mb-0" style="min-width: 80px;">Start Date:</label>
                <input type="date" class="form-control" id="startDate">
            </div>

            <!-- End Date -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="endDate" class="form-label me-2 mb-0" style="min-width: 80px;">End Date:</label>
                <input type="date" class="form-control" id="endDate">
            </div>

            <!-- Cons. St. Date -->
            <div class="col-md-3 d-flex flex-nowrap align-items-center">
                <label for="consStDate" class="form-label me-2 mb-0" style="min-width: 110px;">Cons. St. Date:</label>
                <input type="date" class="form-control" id="consStDate">
            </div>

        </div>
    </form>
</body>
</html>
