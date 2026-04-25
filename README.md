@{
    ViewBag.Title = "PileMatWiseQualityData";
    var data = ViewBag.FinesData as List<dynamic>;
}

<!DOCTYPE html>
<html>
<head>
    <title>PileMatWiseQualityData</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body>

<div class="container mt-4">

    <h3 class="text-center mb-3">Pile Mat Wise Quality Data</h3>

    <table class="table table-bordered text-center">
        <thead class="table-dark">
            <tr>
                <th>Element</th>
                <th>Return Fines</th>
                <th>Wet Fines</th>
                <th>Dry Fines</th>
                <th>Dry Fines 500TPH</th>
            </tr>
        </thead>

        <tbody>

        @if (data != null)
        {
            foreach (var item in data)
            {
                <tr>
                    <td>@item.ELEMENT</td>
                    <td>@item.RETURN_FINES</td>
                    <td>@item.WET_FINES</td>
                    <td>@item.DRY_FINES</td>
                    <td>@item.DRY_FINES_500TPH</td>
                </tr>
            }
        }

        </tbody>
    </table>

    <div class="fw-bold">
        Total Rows: @(data != null ? data.Count : 0)
    </div>

</div>

</body>
</html>
