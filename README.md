@model iMonitor_Web.Models.BF_Production
@{
    Layout = null;

    // Avoid null error
    if (Model == null)
    {
        Model = new iMonitor_Web.Models.BF_Production();
    }
}

<!DOCTYPE html>
<html>
<head>
    <title>BF Production</title>

    <link href="~/css/bootstrap.min.css" rel="stylesheet" />

    <style>
        .page-wrapper {
            max-width: 900px;
            margin: auto;
        }
    </style>
</head>

<body class="bg-white">

<div class="container py-4 page-wrapper">

    <!-- HEADER -->
    <div class="d-flex align-items-center gap-3 mb-3">
        <h4 class="fw-bold mb-0">Production</h4>

        <label>Date</label>

        <!-- IMPORTANT: bind date to model -->
        <input type="date"
               name="DateTime"
               value="@Model.DateTime"
               class="form-control"
               style="width:180px" />
    </div>

    <!-- FORM START -->
    <form method="post">

        <table class="table table-bordered text-center">

            <tr>
                <th>Furnace</th>
                <th>On Date</th>
                <th>To Date</th>
                <th>On Date</th>
                <th>To Date</th>
                <th>Balance</th>
            </tr>

            <!-- CBF -->
            <tr>
                <td><input class="form-control" type="text" name="CBF_Furnace" value="@Model.CBF_Furnace" readonly /></td>
                <td><input class="form-control" type="text" name="CBF_ActOnDate" value="@Model.CBF_ActOnDate" readonly /></td>
                <td><input class="form-control" type="text" name="CBF_ActToDate" value="@Model.CBF_ActToDate" readonly /></td>

                <!-- Editable -->
                <td><input class="form-control" type="text" name="CBF_ReportOnDate" value="@Model.CBF_ReportOnDate" /></td>
                <td><input class="form-control" type="text" name="CBF_ReportToDate" value="@Model.CBF_ReportToDate" /></td>

                <td><input class="form-control" type="text" name="CBF_Balance" value="@Model.CBF_Balance" readonly /></td>
            </tr>

            <!-- EBF -->
            <tr>
                <td><input class="form-control" type="text" name="EBF_Furnace" value="@Model.EBF_Furnace" readonly /></td>
                <td><input class="form-control" type="text" name="EBF_ActOnDate" value="@Model.EBF_ActOnDate" readonly /></td>
                <td><input class="form-control" type="text" name="EBF_ActToDate" value="@Model.EBF_ActToDate" readonly /></td>

                <!-- Editable -->
                <td><input class="form-control" type="text" name="EBF_ReportOnDate" value="@Model.EBF_ReportOnDate" /></td>
                <td><input class="form-control" type="text" name="EBF_ReportToDate" value="@Model.EBF_ReportToDate" /></td>

                <td><input class="form-control" type="text" name="EBF_Balance" value="@Model.EBF_Balance" readonly /></td>
            </tr>

        </table>

        <div class="text-center">
            <button type="submit" class="btn btn-success">Save</button>
        </div>

    </form>
    <!-- FORM END -->

</div>

</body>
</html>
