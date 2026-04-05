@model iMonitor_Web.Models.BF_Production
@{
    Layout = null;
}@*Created BY:- Pabir Kumar Dey
    Created Date:-25-march-2026
    Requested By:-Gaurav Sir.*@
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
                        <input type="date" class="form-control" style="width:150px" value="2026-02-26">
                    </div>
                </div>
                <!-- ===================== MAIN TABLE ===================== -->
                <div class="table-responsive">
                    <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;">
                        <thead>
                            <tr>
                                <th>Date Time</th>
                                <th>Furnace</th>
                                <th>On Date</th>
                                <th>To Date</th>
                                <th>On Date</th>
                                <th>To Date</th>
                                <th>Balance</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
                <!-- ===================== ACTUAL BREAKUP ===================== -->
                <h5 class="mt-4 mb-3 fw-bold border-bottom pb-2" style="font-family:Allan,cursive;">Actual Breakup</h5>
                <div class="table-responsive">
                    <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;">
                        <thead>
                            <tr>
                                <th></th>
                                <th>LD1 Tons</th>
                                <th>LD2 Tons</th>
                                <th>LD3 Tons</th>
                                <th>MRD TP Tons</th>
                                <th>No of TP</th>
                                <th>No of Slag Ladle</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
                <!-- Buttons -->
                <div class="text-center mt-3">
                    <button class="btn btn-success btn-sm">Save</button>
                    <button class="btn btn-info btn-sm">Back</button>
                    <button class="btn btn-primary btn-sm">Raw Mat Cons</button>
                    <button class="btn btn-success btn-sm">Calculate Now</button>
                </div>                   
        
    </div>
</body>
</html>
