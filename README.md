<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Quantity</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .form-label {
            font-weight: 500;
        }
    </style>
</head>
<body>
    <div class="container mt-4">
        <h4 class="mb-4">Raw Material Quantity</h4>

        <form>
            <div class="row mb-3">
                <div class="col-md-2">
                    <label class="form-label">Pile No:</label>
                    <input type="text" class="form-control" placeholder="Pile No">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Source:</label>
                    <input type="text" class="form-control" placeholder="Source">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Shift:</label>
                    <select class="form-select">
                        <option selected>8</option>
                        <option>1</option>
                        <option>2</option>
                        <option>3</option>
                    </select>
                </div>
                <div class="col-md-2">
                    <label class="form-label">Start Date:</label>
                    <input type="date" class="form-control">
                </div>
                <div class="col-md-2">
                    <label class="form-label">End Date:</label>
                    <input type="date" class="form-control">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cons. St. Date:</label>
                    <input type="date" class="form-control">
                </div>
            </div>
            <!-- Add more rows here if needed -->

            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
