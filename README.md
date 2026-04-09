@model iMonitor_Web.Models.BF_Production
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>BF Production</title>
    <!-- Bootstrap 5 -->    
    <link href="~/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/bootstrap-datepicker.min.css" rel="stylesheet" />
    <link href="~/css/all.min.css" rel="stylesheet" />
    <style>
        .page-wrapper {
            max-width: 900px; 
            margin: auto;
        }
    </style>
</head>
<body class="bg-white">
    <div class="container py-4 page-wrapper">                           
                <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-3">
                    <div class="d-flex align-items-center gap-3 flex-wrap">
                        <h4 class="fw-bold mb-0" style="font-family:Allan,cursive;">Production</h4>
                        <label class="fw-semibold">Date</label>
                        <input type="date" class="form-control" style="width:180px" value="2026-02-26">
                    </div>
                </div>
                <!-- ===================== MAIN TABLE ===================== -->
        <form method="post">
            <input type="date" name="DateTime" value="@Model.DateTime" class="form-control" />
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
                    <td><input type="text" name="CBF_Furnace" value="@Model.CBF_Furnace" readonly /></td>
                    <td><input type="text" name="CBF_ActOnDate" value="@Model.CBF_ActOnDate" readonly /></td>
                    <td><input type="text" name="CBF_ActToDate" value="@Model.CBF_ActToDate" readonly /></td>
                    <td><input type="text" name="CBF_ReportOnDate" value="@Model.CBF_ReportOnDate" /></td>
                    <td><input type="text" name="CBF_ReportToDate" value="@Model.CBF_ReportToDate" /></td>
                    <td><input type="text" name="CBF_Balance" value="@Model.CBF_Balance" readonly /></td>
                </tr>
                <!-- EBF -->
                <tr>
                    <td><input type="text" name="EBF_Furnace" value="@Model.EBF_Furnace" readonly /></td>
                    <td><input type="text" name="EBF_ActOnDate" value="@Model.EBF_ActOnDate" readonly /></td>
                    <td><input type="text" name="EBF_ActToDate" value="@Model.EBF_ActToDate" readonly /></td>
                    <td><input type="text" name="EBF_ReportOnDate" value="@Model.EBF_ReportOnDate" /></td>
                    <td><input type="text" name="EBF_ReportToDate" value="@Model.EBF_ReportToDate" /></td>
                    <td><input type="text" name="EBF_Balance" value="@Model.EBF_Balance" readonly /></td>
                </tr>
            </table>
            <button type="submit" class="btn btn-success">Save</button>
        </form>
</div>
</body>
</html>
