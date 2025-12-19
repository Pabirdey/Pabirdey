<!DOCTYPE html>
<html>
<head>
    <title>BF Raw Material Entry</title>
    <!-- Bootstrap CSS -->    
    <link href="~/Bootstrap5/bootstrap.css" rel="stylesheet" /> <style>
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
                    @*<label class="form-label fw-bold">Date</label>
                    <input type="date" class="form-control shadow-sm">*@
                    <span style="font-size:15px;font-family:Century;font-weight:bold">Date</span>
                    <a id="date-daily1" class="drpickr btn btn-o btn-primary">
                        <i class="fa fa-calendar"></i> <label class="value" id="currDate-value" style="font-size:20px;color:blue"></label>
                    </a>
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
    <script src="~/Bootstrap5/jquery-3.7.1.js"></script>
    <script src="~/js/bootstrap-2.3.2.min.js"></script>
    <script src="~/Bootstrap5/jquery.dateandtime.js"></script> 
    <script src="~/js/bootstrap-multiselect.js"></script>   
    <script src="~/js/jquery.min.js"></script>
    <script type="text/javascript">
        let lsSelectedFDate;
        @*$(document).ready(function () {
            $("select").change(function () {
                var furnace = $(this).val();
                loadMaterials(furnace);
            });
            lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            loadMaterials($("select").val());
        });*@
        $('document').ready(function(){
            lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';                    
            $("#From_datepicker").datepicker({
                changeMonth: true,
                changeYear: true,
                setDate: today1,
                format: "dd/mm/yyyy",
                autoclose: true,
                todayHighlight: true
            });
        });
    </script>
    }
</body>
</html>
