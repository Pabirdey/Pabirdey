<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Entry</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container mt-4">

    <h3 class="text-center mb-4">Raw Material Consumption</h3>

    <!-- Date & Furnace Row -->
    <div class="row mb-3">
        <div class="col-md-4">
            <label class="form-label">Date</label>
            <input type="date" class="form-control">
        </div>

        <div class="col-md-4">
            <label class="form-label">Furnace</label>
            <select class="form-select">
                <option>C</option>
                <option>A</option>
                <option>B</option>
            </select>
        </div>
    </div>

    <table class="table table-bordered table-striped">
        <thead class="table-success">
            <tr>
                <th>Material</th>
                <th>Value in Tons</th>
                <th>Value in Kgs</th>
                <th>Type</th>
            </tr>
        </thead>

        <tbody>

            <!-- Example Row 1 -->
            <tr>
                <td>COAL</td>
                <td><input type="text" class="form-control" value="161.460906"></td>
                <td><input type="text" class="form-control" value="161460.906"></td>
                <td>
                    <select class="form-select">
                        <option>IPC</option>
                        <option>Imported</option>
                        <option>Local</option>
                    </select>
                </td>
            </tr>

            <!-- Example Row 2 -->
            <tr>
                <td>NUT COKE</td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td>
                    <select class="form-select">
                        <option>BF Sized Joda</option>
                        <option>Local</option>
                        <option>Other</option>
                    </select>
                </td>
            </tr>

            <!-- Add all other materials same way -->
            <tr>
                <td>PYROXINITE</td>
                <td><input type="text" class="form-control" value="1403.78925"></td>
                <td><input type="text" class="form-control" value="1403789.25"></td>
                <td>
                    <select class="form-select">
                        <option>Local</option>
                        <option>Imported</option>
                    </select>
                </td>
            </tr>

            <tr>
                <td>LIME STONE</td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td>
                    <select class="form-select">
                        <option>Gotan</option>
                        <option>Local</option>
                    </select>
                </td>
            </tr>

        </tbody>
    </table>

    <!-- Buttons -->
    <div class="text-center mt-3">
        <button class="btn btn-primary px-4">Save</button>
        <button class="btn btn-secondary px-4">Back</button>
    </div>

</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

</body>
</html>