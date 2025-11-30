<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Entry</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .medium-textbox {
            width: 120px;
            max-width: 120px;
        }
    </style>
</head>
<body class="bg-light">
    <div class="container mt-4">
        <h3 class="text-center mb-4">Raw Material Consumption</h3>
        <!-- Date & Furnace Row -->
        <div class="row mb-3">
            <div class="col-md-2">
                <label class="form-label">Date</label>
                <input type="date" class="form-control">
            </div>
            <div class="col-md-2">
                <label class="form-label">Furnace</label>
                <select class="form-select">
                    <option>C</option>
                    <option>E</option>
                    <option>F</option>
                </select>
            </div>
        </div>
        <table id="materialTable" class="table table-bordered" style="width:60%;">
            <thead>
                <tr>
                    <th>Material</th>
                    <th>Value (Tons)</th>
                    <th>Value (Kgs)</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
        <div>
            <button class="btn btn-primary px-4">Save</button>
            <button class="btn btn-secondary px-4">Back</button>
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
                                "<td>" + data[i].MATERIAL + "</td>" +
                                "<td><input type='text' class='form-control medium-textbox' value='" + data[i].TONS + "' id='VAL_TONS" + i + "'></td>" +
                                "<td><input type='text' class='form-control medium-textbox' value='" + data[i].KGS + "' id='VAL_KGS" + i + "'></td>" +
                                "</tr>";
                            tbody.append(row);
                        }
                    }
                });
            }
    </script>

</body>
</html>
