<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Entry</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background-color: #f4f6f9;
        }

        .page-title {
            font-weight: 600;
            color: #2c3e50;
        }

        .card-box {
            background: #ffffff;
            padding: 20px;
            border-radius: 14px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.10);
        }

        table {
            background: white;
            border-radius: 10px;
            overflow: hidden;
        }

        thead {
            background: #2c3e50;
            color: white;
        }

        .table tbody tr:hover {
            background: #f1f1f1;
        }

        .medium-textbox {
            width: 120px;
            max-width: 120px;
            text-align: right;
        }

        .btn-custom {
            padding-left: 35px;
            padding-right: 35px;
            font-size: 16px;
            border-radius: 8px;
        }
    </style>
</head>

<body>

    <div class="container mt-5">

        <div class="card-box">

            <h3 class="text-center page-title mb-4">Raw Material Consumption</h3>

            <!-- Date & Furnace Row -->
            <div class="row mb-4">
                <div class="col-md-3">
                    <label class="form-label fw-bold">Date</label>
                    <input type="date" class="form-control shadow-sm">
                </div>

                <div class="col-md-3">
                    <label class="form-label fw-bold">Furnace</label>
                    <select class="form-select shadow-sm">
                        <option>C</option>
                        <option>E</option>
                        <option>F</option>
                    </select>
                </div>
            </div>

            <!-- Table -->
            <table id="materialTable" class="table table-bordered shadow-sm">
                <thead>
                    <tr>
                        <th>Material</th>
                        <th>Value (Tons)</th>
                        <th>Value (Kgs)</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>

            <!-- Buttons -->
            <div class="mt-4">
                <button class="btn btn-primary btn-custom me-2">Save</button>
                <button class="btn btn-secondary btn-custom">Back</button>
            </div>

        </div>

    </div>

    <!-- Scripts -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

    <script>

        $(document).ready(function () {
            $("select").change(function () {
                var furnace = $(this).val();
                loadMaterials(furnace);
            });

            loadMaterials($("select").val());
        });

        function loadMaterials(furnaceName) {
            $.ajax({
                url: '/HML/GetMaterialsByFurnace',
                type: 'GET',
                data: { furnace: furnaceName },
                success: function (data) {

                    var tbody = $("#materialTable tbody");
                    tbody.empty();

                    for (var i = 0; i < data.length; i++) {

                        var row = "<tr>" +
                            "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                            "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].TONS + "'></td>" +
                            "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].KGS + "'></td>" +
                            "</tr>";

                        tbody.append(row);
                    }
                }
            });
        }

    </script>

</body>

</html>
