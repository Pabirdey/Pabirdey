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
    
    .table-bordered td {
        padding: 4px !important;
        vertical-align: middle;
    }
    
    .table-bordered .form-control {
        height: 28px;     
        padding: 2px 5px; 
        font-size: 0.85rem;
        border-radius: 2px;
    }
     .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }

        .datepicker {
            z-index: 1055 !important;
        }
</style>    
</head>
<body class="bg-white">
    <div class="container py-4 page-wrapper">                           
                <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-3">
                    <div class="d-flex align-items-center gap-3 flex-wrap">
                        <h4 class="fw-bold mb-0" style="font-family:Allan,cursive;">Production</h4>                        
                        <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:18px;">Date:&nbsp;</label>
                        <a id="tbFDatePick" class="btn btn-primary">
                            <label id="currDate-value" style="font-size:12px;color:white"></label>
                        </a>
                        <input type="text" id="hiddenDate" style="position:absolute; opacity:0; height:0; width:0;" />
                        &nbsp;&nbsp;&nbsp;&nbsp;
                    </div>
                </div>
                <!-- ===================== MAIN TABLE ===================== -->
        <form method="post">
            <div class="table-responsive" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:15px;">
                <table class="table table-bordered text-center" style="border:2px solid black;">
                    <thead style="border:2px solid black;">
                        <tr>
                            <th>Furnace</th>
                            <th>Actual On Date</th>
                            <th>Actual To Date</th>
                            <th>Reported On Date</th>
                            <th>Reported To Date</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="CBF_Balance" id="CBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="EBF_Furnace" id="EBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="EBF_ActOnDate" id="EBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="EBF_ActToDate" id="EBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="EBF_ReportOnDate" id="EBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="EBF_Balance" id="EBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="FBF_Furnace" id="FBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="FBF_ActOnDate" id="FBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="FBF_ReportOnDate" id="FBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="FBF_Balance" id="FBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="GBF_Furnace" id="GBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="GBF_ActOnDate" id="GBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="GBF_ActToDate" id="GBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="GBF_ReportOnDate" id="GBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="GBF_ReportToDate" id="GBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="GBF_Balance" id="GBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="HBF_Furnace" id="HBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="HBF_ActOnDate" id="HBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="HBF_ActToDate" id="HBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="HBF_ReportOnDate" id="HBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="HBF_ReportToDate" id="HBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="HBF_Balance" id="HBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="IBF_Furnace" id="IBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" onkeyup="calculateAF_ActOnDate()" name="IBF_ActOnDate" id="IBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="IBF_ActToDate" id="IBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="IBF_ReportOnDate" id="IBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="IBF_ReportToDate" id="IBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" name="IBF_Balance" id="IBF_Balance" /></td>
                        </tr>
                        <tr>                           
                            <td>A-F</td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ActOnDate" id="CtoFBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text"  name="CtoFBF_ActToDate" id="CtoFBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ReportOnDate" id="CtoFBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ReportToDate" id="CtoFBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_Balance" id="CtoFBF_Balance" /></td>
                        </tr>
                       
                    </tbody>
                </table>
              </div>

                <!-- ===================== ACTUAL BREAKUP ===================== -->
                <h5 class="mt-4 mb-3 fw-bold border-bottom pb-2" style="font-family:Allan,cursive;">Actual Breakup</h5>
                <div class="table-responsive">
                    <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;font-weight:bold;border:2px solid black;">
                        <thead>
                            <tr>
                                <th></th>
                                <th>LD1 Tons</th>
                                <th>LD2 Tons</th>
                                <th>LD3 Tons</th>
                                <th>MRD TP Tons</th>                                
                            </tr>
                        </thead>
                        <tbody style="font-family:Courier New, Courier, monospace;">
                            <tr>
                                <td><label>On Date</label></td>
                                <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT"  name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>                               
                                
                            </tr>
                            <tr>
                                <td><label>To Date A-F</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-G</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-H</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-I</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>                                
                            </tr>
                        </tbody>
                    </table>
                </div>
                <!-- Buttons -->
                <div class="text-center mt-3">
                    <button class="btn btn-success btn-sm">Save</button>
                    <button class="btn btn-info btn-sm">Back</button>
                    <button class="btn btn-primary btn-sm">Raw Mat Cons</button>
                    <button class="btn btn-success btn-sm">Calculate Now</button>
                </div>
</form>
</div>
<script src="~/js/Jquey3.6.0.min.js"></script>
<script src="~/js/bootstrap.bundle.min.js"></script>
<script src="~/js/bootstrap-datepicker.min.js"></script>
<script>
    let lsSelectedFDate;
    let IsSelectedFur;
    $(document).ready(function () {
        lsSelectedFDate = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').text(lsSelectedFDate);
        $('#hiddenDate').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', lsSelectedFDate);
        $('#tbFDatePick').on('click', function (e) {
            e.preventDefault();
            $('#hiddenDate').datepicker('show');
        });
        $('#hiddenDate').on('changeDate', function (e) {
            lsSelectedFDate = e.format('dd/mm/yyyy');
            $('#currDate-value').text(lsSelectedFDate);
            Display_CTOFBFReportData(lsSelectedFDate);
        });
        Display_CTOFBFReportData(lsSelectedFDate);
        calculateAF_ActOnDate();

      
       
    });

    function Display_CTOFBFReportData(fDate) {
        $.ajax({
            url: '@Url.Action("GetCTOFBFReportDataByFurnace", "HML")',
            type: 'GET',
            data: { fDate: fDate },
            success: function (data) {            
                if (data.message) {
                    alert(data.message);
                    return;
                }

                data.forEach(function (item) {
                    if (item.FURNACE === "C") {                        
                        $("#CBF_Furnace").val(item.FURNACE);
                        $("#CBF_ActOnDate").val(item.ACT_ONDT);
                        $("#CBF_ActToDate").val(item.ACT_TODT);
                        $("#CBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#CBF_ReportToDate").val(item.REPORT_TODT);
                        $("#CBF_Balance").val(item.BALANCE);
                    }

                    if (item.FURNACE === "E") {
                        $("#EBF_Furnace").val(item.FURNACE);
                        $("#EBF_ActOnDate").val(item.ACT_ONDT);
                        $("#EBF_ActToDate").val(item.ACT_TODT);
                        $("#EBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#EBF_ReportToDate").val(item.REPORT_TODT);
                        $("#EBF_Balance").val(item.BALANCE);
                    }

                    if (item.FURNACE === "F") {
                        $("#FBF_Furnace").val(item.FURNACE);
                        $("#FBF_ActOnDate").val(item.ACT_ONDT);
                        $("#FBF_ActToDate").val(item.ACT_TODT);
                        $("#FBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#FBF_ReportToDate").val(item.REPORT_TODT);
                        $("#FBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "G") {
                        $("#GBF_Furnace").val(item.FURNACE);
                        $("#GBF_ActOnDate").val(item.ACT_ONDT);
                        $("#GBF_ActToDate").val(item.ACT_TODT);
                        $("#GBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#GBF_ReportToDate").val(item.REPORT_TODT);
                        $("#GBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "H") {
                        $("#HBF_Furnace").val(item.FURNACE);
                        $("#HBF_ActOnDate").val(item.ACT_ONDT);
                        $("#HBF_ActToDate").val(item.ACT_TODT);
                        $("#HBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#HBF_ReportToDate").val(item.REPORT_TODT);
                        $("#HBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "I") {
                        $("#IBF_Furnace").val(item.FURNACE);
                        $("#IBF_ActOnDate").val(item.ACT_ONDT);
                        $("#IBF_ActToDate").val(item.ACT_TODT);
                        $("#IBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#IBF_ReportToDate").val(item.REPORT_TODT);
                        $("#IBF_Balance").val(item.BALANCE);
                    }

                });
            }
        });

    }
    function calculateAF_ActOnDate() {
        debugger;
        var n1 = parseFloat(document.getElementById("CBF_ActOnDate").value) || 0;
        var n2 = parseFloat(document.getElementById("EBF_ActOnDate").value) || 0;
        var n3 = parseFloat(document.getElementById("FBF_ActOnDate").value) || 0;
        var n4 = parseFloat(document.getElementById("GBF_ActOnDate").value) || 0;
        var n5 = parseFloat(document.getElementById("HBF_ActOnDate").value) || 0;
        var n6 = parseFloat(document.getElementById("IBF_ActOnDate").value) || 0;
        var CtoFBF_ActOnDate = n1 + n2 + n3 + n4 + n5 + n6;
        document.getElementById("CtoFBF_ActOnDate").value = CtoFBF_ActOnDate;
    }
</script>
</body>
</html>
