@model iMonitor_Web.Models.Furnace_High_line
@{
    Layout = null;
}@*Created BY:- Pabir Kumar Dey
    Created Date:-20-April-2026
    Requested By:-Gaurav Sir.*@
<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>
    <!-- Bootstrap -->
    <link href="~/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/bootstrap-datepicker.min.css" rel="stylesheet" />
    <style>
         .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }

        .datepicker {
            z-index: 1055 !important;
        }
        body {
            background: #f4f6f9;
            font-family: Verdana;
            font-size: 12px;
            transform: scale(0.99);
            transform-origin: top left;
        }

        .container-fluid {
            max-width: 1600px;
        }

        /* HEADER */
        .header-box {
            background: #0d47a1;
            color: white;
            padding: 6px;
            border-radius: 6px;
        }

        .header-box h4 {
            font-size: 16px;
        }

        /* SECTION */
        .section-box {
            background: #1976d2;
            color: white;
            padding: 6px;
            border-radius: 6px;
            margin-top: 6px;
        }

        .section-title {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 4px;
        }        
        .table th {
            background: #1565c0;
            color: white;
            font-size: 14px;
            padding: 3px;
        }

        .table td {
            background: white;
            color: black;
            font-size: 14px;
            padding: 3px;
        }        
        .table input,
        .table select {
            width: 100%;
            font-size: 12px;
            height: 24px;
            text-align: center;
        }        
        .table-container input {
            height: 25px;
            font-size: 12px;
            border-radius: 6px;
            padding: 5px;
        }

        .table-custom td {
            vertical-align: middle;
        }

        textarea {
            height: 40px;
            font-size: 11px;
        }

        .form-control,
        .form-select {
            font-size: 12px;
            height: 28px;
        }

        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 10px;
            color: white;
        }

        /* TABS */
        .nav-tabs {
            border-bottom: 2px solid #1976d2;
        }

        .nav-tabs .nav-link {
            color: #1565c0;
            font-weight: 600;
            border-radius: 8px 8px 0 0;
            margin-right: 5px;
            background: #e3f2fd;
        }

        .nav-tabs .nav-link.active {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            color: white !important;
        }

        .tab-pane {
            animation: fadeIn 0.3s ease-in-out;
        }
            select.form-control {
                appearance: auto !important;
                -webkit-appearance: auto !important;
                -moz-appearance: auto !important;
            }  
              /* Small Box */
        .blue-box{
            background:#0066ff;
            border-radius:14px;
            padding:10px 15px;
            display:flex;
            align-items:center;
            justify-content:space-between;
            width:320px;
            margin-top:180px;
            box-shadow:0 3px 8px rgba(0,0,0,0.2);
        }

        .left-section{
            width:58%;
        }

        /* Small Input */
        .custom-input{
            height:27px;
            border:2px solid #999;
            border-radius:5px;
            font-size:13px;
            font-family:Arial;
            font-weight:bold;
            padding-left:10px;
        }

        .custom-input:focus{
            box-shadow:none;
            border-color:#222;
        }

        /* Small Right Section */
        .right-section{
            display:flex;
            align-items:center;
            gap:7px;
            color:white;
            font-size:15px;
            font-weight:600;
            font-family:Arial;
        }

        /* Small Checkbox */
        .form-check-input{
            width:17px;
            height:17px;
            cursor:pointer;
            margin-top:0;
        }

    </style>
    <link href="~/css/Furnace_High_line.css" rel="stylesheet" />
</head>

<body>
    <div class="container-fluid mt-2">        
        <div class="header-box position-relative d-flex align-items-center">            
            <h4 class="m-0 position-absolute start-50 translate-middle-x" style="font-family:Courier New, Courier, monospace;font-weight:bold;font-size:25px;">
                Furnace High Line Log Sheet
            </h4>            
            <div class="ms-auto d-flex gap-2">                
                <label for="tbFDatePick" class="LabelControl" style="font-family:Courier New, Courier, monospace;font-size:22px;font-weight:bold;">Date:&nbsp;</label>
                <a id="tbFDatePick" class="btn btn-primary">
                    <label id="currDate-value" style="font-size:12px;color:white"></label>
                </a>
                <input type="text" id="hiddenDate" style="position:absolute; opacity:0; height:0; width:0;" />
                <select class="form-select" id="ddlshift">
                    <option>A</option>
                    <option>B</option>
                    <option>C</option>
                </select>
            </div>
        </div>
        <!-- TABS -->
        <ul class="nav nav-tabs mt-2">
            <li class="nav-item">
                <a class="nav-link active" data-bs-toggle="tab" href="#tab1">🔥 Coke Unloading</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" data-bs-toggle="tab" href="#tab2">📊 HighLine Log</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" data-bs-toggle="tab" href="#tab3">📦 Bin Position</a>
            </li>
        </ul>
        <!-- TAB CONTENT -->
        <div class="tab-content">
            <!-- TAB 1 -->
            <div class="tab-pane fade show active" id="tab1">
                <div class="row mt-2">
                    <div class="col-md-8">
                        <div class="section-box">
                            <div class="section-title">Coke Unloading</div>
                            <table class="table table-bordered text-center">
                                <thead>
                                    <tr>
                                        <th>Date</th>
                                        <th>Shift</th>
                                        <th>Bunker</th>
                                        <th>C-BF</th>
                                        <th>E-BF</th>
                                        <th>F-BF</th>
                                        <th>Total</th>
                                        <th>Position</th>
                                        <th>Balance</th>
                                    </tr>
                                </thead>
                                <tbody id="tblBody"></tbody>
                            </table>
                        </div>
                        <!-- 🔹 SIDE BY SIDE TABLES -->
                        <div class="row">
                            <!-- Tonnage of Coke -->
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                    <div class="section-title">Tonnage of Coke</div>
                                    <table class="table table-bordered text-center" id="cokeTable">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody>                                                                                                                                                                       
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                            <!-- Tonnage of Nut Coke -->
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                    <div class="section-title">Tonnage of Nut Coke</div>
                                    <table class="table table-bordered text-center" id="nutTable">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody>                                                                                    
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>                                            
                    </div>
                   
                    
                     <div class="col-md-4">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="section-box">
                                    <h7><b>Others</b></h7>
                                    <input class="form-control mb-2" placeholder="Stock Coke Eastern Bunker">
                                    <input class="form-control mb-2" placeholder="Stock Coke Western Bunker">
                                    <input class="form-control mb-2" placeholder="Behive Coke in Middle Bunker">
                                </div>                               
                                <div class="section-box mt-2">
                                    <h7><b>Remarks & Delays</b></h7>
                                    <textarea class="form-control cell" style="height:150px;" data-id="R246"></textarea>
                                </div>   
                                <div class="blue-box">                                 
                                    <div class="left-section">
                                        <input type="text" class="form-control custom-input" list="UserList" id="txtUser" placeholder="Select Users">
                                        <datalist id="UserList">                                           
                                        </datalist>
                                    </div>
                                    <!-- Checkbox -->
                                    <div class="right-section">
                                        <input class="form-check-input" type="checkbox" id="signoff">
                                        <label for="signoff">
                                            Sign OFF
                                        </label>
                                    </div>
                                </div>                      
                            </div>
                            <div class="col-md-6">
                                <div class="section-box">
                                    <h7><b>Coke & Nut Coke Advised & Received</b></h7>
                                    <input class="form-control mb-2 cell" data-id="R50" placeholder="Material advised">
                                    <input class="form-control mb-2 cell" data-id="R51" placeholder="Time advised">
                                    <input class="form-control mb-2 cell" data-id="R52" placeholder="Material received">
                                    <input class="form-control mb-2 cell" data-id="R53" placeholder="Time received">
                                    <input class="form-control mb-2 cell" data-id="R54" placeholder="Unloaded">
                                    <input class="form-control mb-2 cell" data-id="R55" placeholder="Loco left">
                                    <input class="form-control mb-2 cell" data-id="R56" placeholder="Sent down">
                                    <input class="form-control mb-2 cell" data-id="R57" placeholder="Total">
                                </div>
                                <div style="margin-left:100px;margin-top:175px;">
                                    <button class="btn btn-success" id="CokeUnloading"  onclick="SaveCokeUnloading()">
                                        💾 Save
                                    </button>
                                </div>
                            </div>                           
                        </div>                        
                    </div>
                </div>
            </div>

            <!-- TAB 2 -->
            <div class="tab-pane fade" id="tab2">
                <div class="row mt-2">
                    <!-- LEFT PANEL -->
                    <div class="col-md-6">
                        <div class="section-box">
                            <div class="section-title">High Line Log</div>
                            <table class="table table-bordered text-center bg-white text-dark">
                                <thead>
                                    <tr>
                                        <th>Material</th>
                                        <th>Recd.</th>
                                        <th>Retd.</th>
                                        <th style="width:250px;">Reason</th>
                                        <th>U/L</th>
                                        <th style="width:80px;">Balance</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">LRP(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R58"></td>
                                        <td><input type="text" class="form-control cell" data-id="R59"></td>
                                        <td><input type="text" class="form-control cell" data-id="R60"></td>
                                        <td><input type="text" class="form-control cell" data-id="R61" id="R61" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R62" id="R62" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">LRP(IN)</td>
                                        <td><input type="text" class="form-control cell" data-id="R63"></td>
                                        <td><input type="text" class="form-control cell" data-id="R64"></td>
                                        <td><input type="text" class="form-control cell" data-id="R65"></td>
                                        <td><input type="text" class="form-control cell" data-id="R66" id="R66" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R67" id="R67" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">JODA(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R68"></td>
                                        <td><input type="text" class="form-control cell" data-id="R69"></td>
                                        <td><input type="text" class="form-control cell" data-id="R70"></td>
                                        <td><input type="text" class="form-control cell" data-id="R71" id="R71" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R72" id="R72" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">JODA(IN)</td>
                                        <td><input type="text" class="form-control cell" data-id="R73"></td>
                                        <td><input type="text" class="form-control cell" data-id="R74"></td>
                                        <td><input type="text" class="form-control cell" data-id="R75"></td>
                                        <td><input type="text" class="form-control cell" data-id="R76" id="R76" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R77" id="R77" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">TFO</td>
                                        <td><input type="text" class="form-control cell" data-id="R78"></td>
                                        <td><input type="text" class="form-control cell" data-id="R79"></td>
                                        <td><input type="text" class="form-control cell" data-id="R80"></td>
                                        <td><input type="text" class="form-control cell" data-id="R81" id="R81" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R82" id="R82" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">PELLET</td>
                                        <td><input type="text" class="form-control cell" data-id="R351"></td>
                                        <td><input type="text" class="form-control cell" data-id="R352"></td>
                                        <td><input type="text" class="form-control cell" data-id="R353"></td>
                                        <td><input type="text" class="form-control cell" data-id="R354" id="R354" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R355" id="R355" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">SCRAP</td>
                                        <td><input type="text" class="form-control cell" data-id="R88"></td>
                                        <td><input type="text" class="form-control cell" data-id="R89"></td>
                                        <td><input type="text" class="form-control cell" data-id="R90"></td>
                                        <td><input type="text" class="form-control cell" data-id="R91" id="R91" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R92" id="R92" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">L/STONE</td>
                                        <td><input type="text" class="form-control cell" data-id="R93"></td>
                                        <td><input type="text" class="form-control cell" data-id="R94"></td>
                                        <td><input type="text" class="form-control cell" data-id="R95"></td>
                                        <td><input type="text" class="form-control cell" data-id="R96" id="R96" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R97" id="R97" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">PYROXINITE</td>
                                        <td><input type="text" class="form-control cell" data-id="R98"></td>
                                        <td><input type="text" class="form-control cell" data-id="R99"></td>
                                        <td><input type="text" class="form-control cell" data-id="R100"></td>
                                        <td><input type="text" class="form-control cell" data-id="R101" id="R101" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R102" id="R102" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">QUARTZ</td>
                                        <td><input type="text" class="form-control cell" data-id="R103"></td>
                                        <td><input type="text" class="form-control cell" data-id="R104"></td>
                                        <td><input type="text" class="form-control cell" data-id="R105"></td>
                                        <td><input type="text" class="form-control cell" data-id="R106" id="R106" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R107" id="R107" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">NUT COKE</td>
                                        <td><input type="text" class="form-control cell" data-id="R108"></td>
                                        <td><input type="text" class="form-control cell" data-id="R109"></td>
                                        <td><input type="text" class="form-control cell" data-id="R110"></td>
                                        <td><input type="text" class="form-control cell" data-id="R111" id="R111" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R112" id="R112" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">STOCK SINTER</td>
                                        <td><input type="text" class="form-control cell" data-id="R113"></td>
                                        <td><input type="text" class="form-control cell" data-id="R114"></td>
                                        <td><input type="text" class="form-control cell" data-id="R115"></td>
                                        <td><input type="text" class="form-control cell" data-id="R116" id="R116" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R117" id="R117" onblur="TotBal()"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1" style="font-family:Courier New, Courier, monospace;font-weight:bold;">SINTER(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R271"></td>
                                        <td><input type="text" class="form-control cell" data-id="R272"></td>
                                        <td><input type="text" class="form-control cell" data-id="R273"></td>
                                        <td><input type="text" class="form-control cell" data-id="R274" id="R274" onblur="TotUL()"></td>
                                        <td><input type="text" class="form-control cell" data-id="R275" id="R275" onblur="TotBal()"></td>
                                    </tr>
                                </tbody>
                            </table>
                            <div class="text-end">
                                <strong style="margin-left:490px;">Total</strong><input type="text" id="txtTotul" style="width:90px;margin-left:50px;" /><input type="text" style="width:90px;"/>
                            </div>
                        </div>
                        <div class="section-box mt-2">
                            <h6>Remarks & Delays</h6>
                            <textarea class="form-control"></textarea>
                        </div>
                    </div>

                    <!-- CENTER PANEL -->
                    <div class="col-md-3">
                        <div class="section-box">
                            <div class="section-title"><span style="margin-left:150px;">C-BF</span></div>
                            <table class="table table-bordered text-center bg-white text-dark">
                                <thead>
                                    <tr>
                                        <th></th>
                                        <th>DMAG</th>
                                        <th>KO</th>
                                        <th>BELT</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>SP1</td>
                                        <td><input type="text" class="form-control cell" data-id="R120"></td>
                                        <td><input type="text" class="form-control cell" data-id="R280"></td>
                                        <td><input type="text" class="form-control cell" data-id="R281"></td>
                                    </tr>
                                    <tr>
                                        <td>SP2</td>
                                        <td><input type="text" class="form-control cell" data-id="R126"></td>
                                        <td><input type="text" class="form-control cell" data-id="R292"></td>
                                        <td><input type="text" class="form-control cell" data-id="R293"></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        <div class="section-box">
                            <div class="section-title"><span style="margin-left:150px;">E-BF</span></div>
                            <table class="table table-bordered text-center bg-white text-dark">
                                <thead>
                                    <tr>
                                        <th></th>
                                        <th>DMAG</th>
                                        <th>KO</th>
                                        <th>BELT</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>SP1</td>
                                        <td><input type="text" class="form-control cell" data-id="R122"></td>
                                        <td><input type="text" class="form-control cell" data-id="R284"></td>
                                        <td><input type="text" class="form-control cell" data-id="R285"></td>
                                    </tr>
                                    <tr>
                                        <td>SP2</td>
                                        <td><input type="text" class="form-control cell" data-id="R128"></td>
                                        <td><input type="text" class="form-control cell" data-id="R296"></td>
                                        <td><input type="text" class="form-control cell" data-id="R297"></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        <div class="section-box">
                            <div class="section-title"><span style="margin-left:150px;">F-BF</span></div>
                            <table class="table table-bordered text-center bg-white text-dark">
                                <thead>
                                    <tr>
                                        <th></th>
                                        <th>DMAG</th>
                                        <th>KO</th>
                                        <th>BELT</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>SP1</td>
                                        <td><input type="text" class="form-control cell" data-id="R123"></td>
                                        <td><input type="text" class="form-control cell" data-id="R286"></td>
                                        <td><input type="text" class="form-control cell" data-id="R287"></td>
                                    </tr>
                                    <tr>
                                        <td>SP2</td>
                                        <td><input type="text" class="form-control cell" data-id="R129"></td>
                                        <td><input type="text" class="form-control cell" data-id="R298"></td>
                                        <td><input type="text" class="form-control cell" data-id="R299"></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        <div class="section-box">
                            <div class="section-title"><span style="margin-left:150px;">TOTAL</span></div>
                            <table class="table table-bordered text-center bg-white text-dark">
                                <thead>
                                    <tr>
                                        <th></th>
                                        <th>DMAG</th>
                                        <th>KO</th>
                                        <th>BELT</th>
                                        <th>TOT</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>SP1</td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                    </tr>
                                    <tr>
                                        <td>SP2</td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                        <td><input type="text" class="form-control cell" readonly></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <!-- RIGHT PANEL -->
                    <div class="col-md-3">
                        <div class="section-box" style="height:145px;">
                            <div class="section-title">Sinter Storage</div>
                            <!-- ROW 1: SP1 + SP2 -->
                            <div class="row align-items-center mb-2">
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">SP1</label>
                                    <input type="text" class="form-control cell" data-id="R130" style="width:80px;">
                                </div>
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">SP2</label>
                                    <input type="text" class="form-control cell" data-id="R131" style="width:80px;">
                                </div>
                            </div>
                            <!-- ROW 2: TOTAL -->
                            <div class="row align-items-center mb-2">
                                <div class="col-md-12 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">Total Fines(t)</label>
                                    <input type="text" class="form-control cell" data-id="R300" style="width:80px;">
                                </div>
                            </div>

                            <!-- ROW 3: PERCENTAGE -->
                            <div class="row align-items-center">

                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">SP1 Fines(%)</label>
                                    <input type="text" class="form-control cell" data-id="R301" readonly style="width:80px;">
                                </div>
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">SP2 Fines(%)</label>
                                    <input type="text" class="form-control cell" data-id="R302" style="width:80px;">
                                </div>

                            </div>
                        </div>
                        <div class="section-box" style="height:135px;">
                            <div class="section-title">Reclaimed Ore</div>
                            <!-- ROW 1: SP1 + SP2 -->
                            <div class="row align-items-center mb-2">
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">LRP</label>
                                    <input type="text" class="form-control cell" data-id="R132" style="width:80px;">
                                </div>
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">JODA</label>
                                    <input type="text" class="form-control cell" data-id="R133" style="width:80px;">
                                </div>
                            </div>                         
                            <!-- ROW 3: PERCENTAGE -->
                            <div class="row align-items-center">
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">Direct Fines</label>
                                    <input type="text" class="form-control cell" data-id="R303" style="width:80px;">
                                </div>
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">Direct Fines</label>
                                    <input type="text" class="form-control cell" data-id="R304" style="width:80px;">
                                </div>
                            </div>
                            <div class="row align-items-center">
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">Reclaimed Fines</label>
                                    <input type="text" class="form-control cell" data-id="R305" style="width:80px;">
                                </div>
                                <div class="col-md-6 d-flex align-items-center gap-2">
                                    <label style="width:70px; color:white;font-weight:bold;">Reclaimed Fines</label>
                                    <input type="text" class="form-control cell" data-id="R306" style="width:80px;">
                                </div>
                            </div>
                        </div>
                        <div class="section-box">
                            <div class="section-title">FLB Data</div>
                            <table class="table table-bordered bg-white text-dark">
                                <tr>
                                    <th>SlNo</th>
                                    <th>Material</th>
                                    <th>FLB Position</th>
                                </tr>
                                <tr>
                                    <td>1</td>
                                    <td>
                                        <select class="form-select cell" data-id="R134" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 cell" data-id="R135"></td>
                                </tr>
                                <tr>
                                    <td>2</td>
                                    <td>
                                        <select class="form-select cell" data-id="R136" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 form-control-sm cell" data-id="R137"></td>
                                </tr>
                                <tr>
                                    <td>3</td>
                                    <td>
                                        <select class="form-select cell" data-id="R138" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 form-control-sm cell" data-id="R139"></td>
                                </tr>
                                <tr>
                                    <td>4</td>
                                    <td>
                                        <select class="form-select cell" data-id="R140" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 form-control-sm cell" data-id="R141"></td>
                                </tr>
                                <tr>
                                    <td>5</td>
                                    <td>
                                        <select class="form-select cell" data-id="R142" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 form-control-sm cell" data-id="R143"></td>
                                </tr>
                                <tr>
                                    <td>6</td>
                                    <td>
                                        <select class="form-select cell" data-id="R144" style="height:30px;width:150px;text-align:left;">
                                            <option></option>
                                            <option>LRP</option>
                                            <option>JODA</option>
                                            <option>SINTER</option>
                                            <option>QUARTZITE</option>
                                            <option>PYROXINITE</option>
                                            <option>TFO</option>
                                            <option>NUT COKE</option>
                                            <option>LIMESTONE</option>
                                            <option>SCRAP</option>
                                            <option>SPONGE IRON</option>
                                        </select>
                                    </td>
                                    <td><input type="text" class="form-control text-start p-2 form-control-sm cell" data-id="R145"></td>
                                </tr>
                            </table>
                        </div>                         
                    </div>                  
                      <div class="text-center mt-1">
                       <button class="btn btn-success" onclick="SaveFurnaceHighLine()">
                                💾 Save
                        </button>            
                    </div>              
                </div>
            </div>
            <!-- TAB 3 -->
            <div class="tab-pane fade" id="tab3">
                <div class="container mt-4">
                    <div class="card-custom" style="width:900px;">
                        <div class="mb-3 position-relative">                            
                            <h4 class="text-center m-0 fw-bold" style="font-size:22px;">
                                Raw Material Position
                            </h4>                                                      
                        </div>
                        <div class="table-container">
                            <table class="table table-bordered table-custom">
                                <thead class="font-size:12px;">
                                    <tr>
                                        <th>Material</th>
                                        <th style="width:120px;">Yard Position</th>
                                        <th style="width:120px;">H.L.Position</th>
                                        <th style="width:120px;">Stock Loaded</th>
                                        <th style="width:120px;">C-BF</th>
                                        <th style="width:120px;">E-BF</th>
                                        <th style="width:120px;">F-BF</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td class="material-name">Sinter</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R147"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R148"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R149"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R152"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R154"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R155"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">TFO</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R156"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R157"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R158"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R161"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R163"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R164"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">LRP</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R165"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R166"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R167"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R170"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R172"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R173"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Joda</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R174"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R175"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R176"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R179"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R181"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R182"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Pellet</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R383"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R384"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R385"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R388"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R390"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R391"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Nut Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R192"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R193"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R194"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R197"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R199"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R200"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Limestone</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R201"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R202"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R203"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R206"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R208"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R209"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Pyroxinite</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R210"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R211"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R212"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R215"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R217"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R218"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">ORT</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R219"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R220"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R221"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R224"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R226"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R227"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Scrap</td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R228"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R229"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R230"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R233"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R235"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R236"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Coke(On Stock)</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R237"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R238"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R239"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R242"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R244"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R245"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Low Ash Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R307"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R308"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R309"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R312"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R314"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R315"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">High Ash Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R316"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R317"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R318"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R321"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R323"></td>
                                        <td><input type="text" class="form-control cell text-start ps-5" data-id="R324"></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>

                    </div>
                </div>
                <button class="btn btn-success" style="margin-left:500px;margin-top:10px;" onclick="SaveFurnaceBinPosition()">
                    💾 Save
                </button>
            </div>

        </div>    
       
     </div>    
    <!-- Loader -->
    <div class="loader-container" id="loaderDiv">
        <div class="loader"></div>
    </div>   
    <script src="~/js/Jquey3.6.0.min.js"></script>
    <script src="~/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/bootstrap-datepicker.min.js"></script>
    <script>
        let lsSelectedFDate;        
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
                loadUsers();
                Display_Bin_Position();
                copyDateShiftToRows();
                Display_Coke_unloading();  
                LoadTonnageFromDB();
            });
            $('#ddlshift').on('change', function () {
                loadUsers();
                loadShiftData();
                Display_Bin_Position();
                copyDateShiftToRows();
                Display_Coke_unloading(); 
                LoadTonnageFromDB();
            });
            $("#loaderDiv").hide();
            loadUsers();
            Display_Bin_Position();
            copyDateShiftToRows();  
            Display_Coke_unloading();  
            LoadTonnageFromDB();
            TotUL();         
        });        
    </script>
   <script>  
       function TotUL() {            
           var n1 = parseFloat(document.getElementById("R61").value) || 0;
           var n2 = parseFloat(document.getElementById("R66").value) || 0;
           var n3 = parseFloat(document.getElementById("R71").value) || 0;
           var n4 = parseFloat(document.getElementById("R76").value) || 0;
           var n5 = parseFloat(document.getElementById("R81").value) || 0;        
           var n6 = parseFloat(document.getElementById("R354").value) || 0;        
           var n7 = parseFloat(document.getElementById("R91").value) || 0;        
           var n8 = parseFloat(document.getElementById("R96").value) || 0;        
           var n9 = parseFloat(document.getElementById("R101").value) || 0;        
           var n10 = parseFloat(document.getElementById("R106").value) || 0;        
           var n11 = parseFloat(document.getElementById("R111").value) || 0;        
           var n12= parseFloat(document.getElementById("R116").value) || 0;        
           var n13 = parseFloat(document.getElementById("R274").value) || 0;                        
           var ULTOT= n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11 + n12 + n13;
           document.getElementById("txtTotul").value = ULTOT;
       }                 
       function Display_Bin_Position() {           
           var shift = $("#ddlshift").val();
           $.ajax({
               url: '/Furnace_High_line/Get_Bin_Position',
               type: 'GET',
               data: { date: lsSelectedFDate, shift: shift },
               success: function (res) {
                   console.log(res);
                   if (res.success) {
                       $(".cell").val("");
                       res.data.forEach(function (item) {
                           var id = item.CellId ? item.CellId.trim() : "";                           
                           var inputs = document.querySelectorAll('.cell[data-id="' + id + '"]');
                           if (inputs.length > 0) {
                               inputs.forEach(function (input) {
                                   input.value = item.Value;
                               });
                           } else {
                               console.warn("No matching element for:", id);
                           }
                       });

                   } else {
                       alert(res.message);
                   }
               },

               error: function () {
                   alert("Error Loading Data");
               }
           });
       }

       function Display_Coke_unloading() {
           var shift = $("#ddlshift").val();
           $.ajax({
               url: '/Furnace_High_line/Get_Coke_Unloading',
               type: 'GET',
               data: {
                   date: lsSelectedFDate,
                   shift: shift
               },
               success: function (res) {
                   let tbody = $("#tblBody");
                   tbody.empty();
                   if (res.success && res.data.length > 0) {                       
                       res.data.forEach(function (item) {
                           tbody.append(createRow(item));
                       });

                   } else {                       
                       for (let i = 0; i < 8; i++) {
                           tbody.append(createRow());
                       }
                   }
                   
                   copyDateShiftToRows();
                   LoadTonnageFromDB();
               },
               error: function () {
                   alert("Error loading data");
               }
           });
       }

                   
       function SaveFurnaceBinPosition() {
           $("#loaderDiv").show();
           var list = [];
           var shift = $("#ddlshift").val();
           var selectedIds = ["R147","R148","R149","R152","R154","R155","R156","R157","R158","R161","R163","R164","R165","R166","R167","R170",
                              "R172","R173","R174","R175","R176","R179","R181","R182","R383","R384","R385","R388","R390","R391","R192","R193",
                              "R194","R197","R199","R200","R201","R202","R203","R206","R208","R209","R210","R211","R212","R215","R217","R218",
                              "R219","R220","R221","R224","R226","R227","R228","R229","R230","R233","R235","R236","R237","R238","R239","R242",
                              "R244","R245","R307","R308","R309","R312","R314","R315","R316","R317","R318","R321","R323","R324"];          
           $(".cell").each(function () {                             
               var id = $(this).data("id"); 
               var value = $(this).val();               
               if(selectedIds.includes(id)){
                   list.push({                   
                       CellId: id,
                       Value: value,
                       Date: lsSelectedFDate,
                       Shift: shift
                   });         
               }
           });        

           console.log(list);
           $.ajax({
               url: '/Furnace_High_line/Save_Furnace_Bin_Position',
               type: 'POST',
               data: JSON.stringify({ list: list }),  
               contentType: 'application/json',
               success: function (res) {
                   if (res.success) {
                       alert(res.message);  
                       $("#loaderDiv").hide();
                   }
                   else {
                       alert(res.message);
                   }
               },

               error: function () {
                   alert("Save failed!");
                   $("#loaderDiv").hide();
               }
           });
       }

       function SaveFurnaceCokeUnloading_ID() {
           var list = [];
           var shift = $("#ddlshift").val();
           var selectedIds = ["R246","R50","R51","R52","R53","R54","R55","R56","R57"];          
           $(".cell").each(function () {                             
               var id = $(this).data("id"); 
               var value = $(this).val();               
               if(selectedIds.includes(id)){
                   list.push({                   
                       CellId: id,
                       Value: value,
                       Date: lsSelectedFDate,
                       Shift: shift
                   });         
               }
           });        

           console.log(list);
           $.ajax({
               url: '/Furnace_High_line/Save_Furnace_CokeUnloading',
               type: 'POST',
               data: JSON.stringify({ list: list }),  
               contentType: 'application/json',
               success: function (res) {
                   if (res.success) {
                       alert(res.message);  
                       $("#loaderDiv").hide();

                   }
                   else {
                       alert(res.message);
                   }
               },

               error: function () {
                   $("#loaderDiv").hide();
               }
           });
       }

       
       function SaveFurnaceHighLine() {   
           $("#loaderDiv").show();
           var list = [];
           var shift = $("#ddlshift").val();              
           var selectedIds = [
               "R58","R59","R60","R61","R62","R63","R64","R65","R66","R67","R68","R69","R70","R71","R72","R73","R74","R75","R76",
               "R77","R78","R79","R80","R81","R82","R351","R352","R353","R354","R355","R88","R89","R90","R91","R92","R93","R94",
               "R95","R96","R97","R98","R99","R100","R101","R102","R103","R104","R105","R106","R107","R108","R109","R110","R111",
               "R112","R113","R114","R115","R116","R117","R271","R272","R273","R274","R275","R120","R280","R281","R126","R292",
               "R293","R122","R284","R285","R128","R296","R297","R123","R286","R287","R129","R298","R299","R130","R131","R300",
               "R301","R302","R132","R133","R303","R304","R305","R306","R134","R135","R136","R137","R138","R139","R140","R141",
               "R142","R143","R144","R145"
           ];

           $(".cell").each(function () {                             
               var id = $(this).data("id"); 
               var value = $(this).val();               
               if(selectedIds.includes(id)){
                   list.push({                   
                       CellId: id,
                       Value: value,
                       Date: lsSelectedFDate,
                       Shift: shift
                   });         
               }
           });            

           console.log("Data to send:", list);
           if (list.length === 0) {
               alert("No data to save!");
               return;
           }

           $.ajax({
               url: '/Furnace_High_line/Save_Furnace_Highline',
               type: 'POST',
               data: JSON.stringify({ list: list }),  
               contentType: 'application/json; charset=utf-8',
               success: function (res) {                 
                   alert(res.message);
                   $("#loaderDiv").hide();
               },
               error: function (xhr, status, error) {
                   console.error("Error details:", error);
                   $("#loaderDiv").hide();
               }
           });
       }      
   </script>              
<script>
    function createRow(item = {}) {      
    return `
    <tr>
        <td><input type="text" class="form-control row-date" style="width:100px;" value="${formatDate(item.TIMESTAMP)}" readonly></td>

        <td>
            <select class="form-control row-shift" style="height:30px;width:50px;">
                <option ${item.SHIFT==='A'?'selected':''}>A</option>
                <option ${item.SHIFT==='B'?'selected':''}>B</option>
                <option ${item.SHIFT==='C'?'selected':''}>C</option>
            </select>
        </td>

        <td>
            <select class ="form-control bunker text-start ps-01" style="height:30px;width:200px;" onchange="LoadTonnageFromDB()">
                <option value="">---Pls. Select---</option>
                <option value="WESTERN" ${item.BUNKER==='WESTERN'?'selected':''}>WESTERN</option>
                <option value="H/S NC" ${item.BUNKER==='H/S NC'?'selected':''}>H/S NC</option>
                <option value="ST.COKE - TOTAL" ${item.BUNKER==='ST.COKE - TOTAL'?'selected':''}>ST.COKE - TOTAL</option>
                <option value="EASTERN" ${item.BUNKER==='EASTERN'?'selected':''}>EASTERN</option>
                <option value="ST.COKE - HALDIA" ${item.BUNKER==='ST.COKE - HALDIA'?'selected':''}>ST.COKE - HALDIA</option>
                <option value="MIDDLE" ${item.BUNKER==='MIDDLE'?'selected':''}>MIDDLE</option>
                <option value="B/H COKE - TOTAL" ${item.BUNKER==='B/H COKE - TOTAL'?'selected':''}>B/H COKE - TOTAL</option>
                <option value="ST.COKE" ${item.BUNKER==='ST.COKE'?'selected':''}>ST.COKE</option>
                <option value="B/H LOW ASH" ${item.BUNKER==='B/H LOW ASH'?'selected':''}>B/H LOW ASH</option>
                <option value="NC BF KO" ${item.BUNKER==='NC BF KO'?'selected':''}>NC BF KO</option>
                <option value="ROUGH BREEZE" ${item.BUNKER==='ROUGH BREEZE'?'selected':''}>ROUGH BREEZE</option>
                <option value="PLS_25MM_NC" ${item.BUNKER==='PLS_25MM_NC'?'selected':''}>PLS_25MM_NC</option>
                <option value="ST.COKE - IMPORTED" ${item.BUNKER==='ST.COKE - IMPORTED'?'selected':''}>ST.COKE - IMPORTED</option>
                <option value="B/H HIGH ASH" ${item.BUNKER==='B/H HIGH ASH'?'selected':''}>B/H HIGH ASH</option>
                <option value="ST.COKE - OWN" ${item.BUNKER==='ST.COKE - OWN'?'selected':''}>ST.COKE - OWN</option>
            </select>
        </td>

        <td><input type="text" class="form-control c" value="${item.C || ''}"></td>
        <td><input type="text" class="form-control e" value="${item.E || ''}"></td>
        <td><input type="text" class="form-control f" value="${item.F || ''}"></td>

        <td><input type="text" class="form-control total" value="${item.TOTAL || ''}" readonly></td>

        <td><input type="text" class="form-control position" value="${item.BUNKER_POSITION || ''}"></td>
        <td><input type="text" class="form-control balance" value="${item.BALANCE || ''}"></td>
    </tr>`;
            }

       function copyDateShiftToRows() {         
           var headerDate = document.getElementById("hiddenDate").value;
           var headerShift = document.getElementById("ddlshift").value;          
           document.querySelectorAll("#tblBody tr").forEach(function (row) {
               var dateInput = row.querySelector(".row-date");
               var shiftSelect = row.querySelector(".row-shift");
               if (dateInput) dateInput.value = headerDate;
               if (shiftSelect) shiftSelect.value = headerShift;

           });           
            }
       function formatDate(dt) {
           if (!dt) return "";
           let d = new Date(dt);
           let day = ("0" + d.getDate()).slice(-2);
           let month = ("0" + (d.getMonth() + 1)).slice(-2);
           let year = d.getFullYear();
           return day + "/" + month + "/" + year;
       }       
</script>
@*<script>
function LoadTonnageFromDB() {
  var shift = $("#ddlshift").val();
  var date = lsSelectedFDate;                    
  var bunkers = [];
                    $(".bunker").each(function () {
                        var val = $(this).val();
                        if (val && !bunkers.includes(val)) {
                            bunkers.push(val);
                        }
                    });
                    if (!date || !shift || bunkers.length === 0) {
                        return;
                    }

                    $.ajax({
                        url: "/Furnace_High_line/GetTonnageData",
                        type: "GET",
                        data: { date: date, shift: shift },

                        success: function (data) {
                            if (!data.success) {
                                alert(data.message);
                                return;
                            }

                            var cokeBody = $("#cokeTable tbody");
                            var nutBody = $("#nutTable tbody");

                            cokeBody.html("");
                            nutBody.html("");                         
                            for (var b = 0; b < bunkers.length; b++) {
                                var bunker = bunkers[b];                                
                                var cokeRow = null;
                                for (var i = 0; i < data.coke.length; i++) {
                                    if (data.coke[i].BUNKER === bunker) {
                                        cokeRow = data.coke[i];
                                        break;
                                    }
                                }                                
                                var nutRow = null;
                                for (var j = 0; j < data.nut.length; j++) {
                                    if (data.nut[j].BUNKER === bunker) {
                                        nutRow = data.nut[j];
                                        break;
                                    }
                                }                               
                                cokeBody.append(
                                                 "<tr>" +
                                                 "<td>" + bunker + "</td>" +
                                                 "<td><input type='number' class='form-control c' readonly value='" + (cokeRow ? getVal(cokeRow.C) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control e' readonly value='" + (cokeRow ? getVal(cokeRow.E) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control f' readonly value='" + (cokeRow ? getVal(cokeRow.F) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control total' readonly></td>" +
                                                 "</tr>"
                                             );

                                    nutBody.append(
                                            "<tr>" +
                                            "<td>" + bunker + "</td>" +
                                            "<td><input type='number' class='form-control c' readonly value='" + (nutRow ? getVal(nutRow.C) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control e' readonly value='" + (nutRow ? getVal(nutRow.E) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control f' readonly value='" + (nutRow ? getVal(nutRow.F) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control total' readonly></td>" +
                                            "</tr>"
                                );
                            }                          
                            $("#cokeTable input, #nutTable input").on("input", calculateTotal);                            
                            calculateAllTotals();
                        }
                    });
                }
                function calculateTotal() {
                    var row = this.closest("tr");
                    var c = parseFloat(row.querySelector(".c").value) || 0;
                    var e = parseFloat(row.querySelector(".e").value) || 0;
                    var f = parseFloat(row.querySelector(".f").value) || 0;

                    row.querySelector(".total").value = c + e + f;
                }

                function calculateAllTotals() {
                    document.querySelectorAll("#cokeTable tr, #nutTable tr").forEach(function (row) {
                        var c = parseFloat(row.querySelector(".c")?.value) || 0;
                        var e = parseFloat(row.querySelector(".e")?.value) || 0;
                        var f = parseFloat(row.querySelector(".f")?.value) || 0;

                        var totalInput = row.querySelector(".total");
                        if (totalInput) {
                            totalInput.value = c + e + f;
                        }
                    });
                }
    
                function getVal(val) {
                    return (val === null || val === undefined) ? "" : val;
                }



</script>*@
<script>
    function SaveCokeUnloading() {
        $("#loaderDiv").show();
        var mainList = [];
        var cokeList = [];
        var nutList = [];    
        var mainRows = document.querySelectorAll("#tblBody tr");
        for (var i = 0; i < mainRows.length; i++) {
            var row = mainRows[i];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Shift: row.querySelector(".row-shift").value,
                Bunker: row.querySelector(".bunker").value,

                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,

                Total: row.querySelector(".total").value,
                Position: row.querySelector(".position").value,
                Balance: row.querySelector(".balance").value
            };

            mainList.push(obj);
        }    
        var cokeRows = document.querySelectorAll("#cokeTable tbody tr");
        for (var j = 0; j < cokeRows.length; j++) {
            var row = cokeRows[j];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            cokeList.push(obj);
        }

        var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }

        console.log("MAIN:", mainList);
        console.log("COKE:", cokeList);
        console.log("NUT:", nutList); 
        $.ajax({
            url: '/Furnace_High_line/SaveFurnaceCokeUnloading',
            type: 'POST',
            data: JSON.stringify({
                main: mainList,
                coke: cokeList,
                nut: nutList
            }),
            contentType: 'application/json',
            success: function () {
               // Furnace_Line_Coke_Unloading();
                SaveFurnaceCokeUnloading_ID();
            },
            error: function () {
                alert("Error Saving Data");
            }
        });
    }
    function Furnace_Line_Coke_Unloading() {          
        var shift=$("#ddlshift").val();
        var furnaces = ["C", "E", "F"];
        $("#msg").text("Processing...");            
        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/Furnace_High_line/CallProcedure_Coke_Distribution',
                type: 'POST',
                data: {
                    p_date:lsSelectedFDate,
                    p_furnace: furnace,
                    P_shift:shift
                },
                success: function (res) {                   
                },
                error: function () {                    
                }
            });

        });
    }
</script>
<script>
    function LoadTonnageFromDB() {        
        var shift = $("#ddlshift").val();

        var date = lsSelectedFDate;

        var bunkers = [];

        $(".bunker").each(function () {

            var val = $(this).val();

            if (val && !bunkers.includes(val)) {

                bunkers.push(val);
            }
        });

        if (!date || !shift || bunkers.length === 0) {

            return;
        }

        $.ajax({

            url: "/Furnace_High_line/GetTonnageData",

            type: "GET",

            data: { date: date, shift: shift },

            success: function (data) {

                if (!data.success) {

                    alert(data.message);

                    return;
                }                
                var cokeBody = $("#cokeTable tbody");

                var nutBody = $("#nutTable tbody");

                cokeBody.empty();

                nutBody.empty();

                // =========================================
                // TOTAL VARIABLES
                // =========================================

                var TOTAL_TON_SC_S = 0;

                var TOTAL_TON_NC_H = 0;

                var TOTAL_TON_NC_BF_KO = 0;

                var TOTAL_TON_NC_P25 = 0;

                // =========================================
                // LOOP BUNKERS
                // =========================================

                for (var b = 0; b < bunkers.length; b++) {

                    var bunker = bunkers[b];

                    var cokeRow = null;

                    for (var i = 0; i < data.coke.length; i++) {

                        if (data.coke[i].BUNKER === bunker) {

                            cokeRow = data.coke[i];

                            break;
                        }
                    }

                    var nutRow = null;

                    for (var j = 0; j < data.nut.length; j++) {

                        if (data.nut[j].BUNKER === bunker) {

                            nutRow = data.nut[j];

                            break;
                        }
                    }

                    // =========================================
                    // VALUES
                    // =========================================

                    var c = parseFloat(cokeRow?.C || nutRow?.C || 0);

                    var e = parseFloat(cokeRow?.E || nutRow?.E || 0);

                    var f = parseFloat(cokeRow?.F || nutRow?.F || 0);

                    var total = c + e + f;

                    // =========================================
                    // ST.COKE
                    // =========================================

                    if (bunker.substring(0, 7) === "ST.COKE") {

                        var cVal = c * 40;

                        var eVal = e * 40;

                        var fVal = f * 40;

                        var rowTotal = cVal + eVal + fVal;

                        TOTAL_TON_SC_S += rowTotal;

                        cokeBody.append(

                            "<tr>" +

                            "<td>" + bunker + "</td>" +

                            "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                            "</tr>"
                        );
                    }

                        // =========================================
                        // H/S NC
                        // =========================================

                    else if (bunker === "H/S NC") {

                        var cVal = c * 21;

                        var eVal = e * 21;

                        var fVal = f * 21;

                        var rowTotal = cVal + eVal + fVal;

                        TOTAL_TON_NC_H += rowTotal;

                        nutBody.append(

                            "<tr>" +

                            "<td>" + bunker + "</td>" +

                            "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                            "</tr>"
                        );
                    }

                        // =========================================
                        // NC BF KO
                        // =========================================

                    else if (bunker === "NC BF KO") {

                        var cVal = c * 12;

                        var eVal = e * 12;

                        var fVal = f * 12;

                        var rowTotal = cVal + eVal + fVal;

                        TOTAL_TON_NC_BF_KO += rowTotal;

                        nutBody.append(

                            "<tr>" +

                            "<td>" + bunker + "</td>" +

                            "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                            "</tr>"
                        );
                    }

                        // =========================================
                        // PLS_25MM_NC
                        // =========================================

                    else if (bunker === "PLS_25MM_NC") {

                        var cVal = c * 40;

                        var eVal = e * 40;

                        var fVal = f * 40;

                        var rowTotal = cVal + eVal + fVal;

                        TOTAL_TON_NC_P25 += rowTotal;

                        nutBody.append(

                            "<tr>" +

                            "<td>" + bunker + "</td>" +

                            "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                            "</tr>"
                        );
                    }

                        // =========================================
                        // OTHER BUNKERS
                        // =========================================

                    else {

                        cokeBody.append(

                            "<tr>" +

                            "<td>" + bunker + "</td>" +

                            "<td><input type='number' class='form-control c' readonly value='" + c + "'></td>" +

                            "<td><input type='number' class='form-control e' readonly value='" + e + "'></td>" +

                            "<td><input type='number' class='form-control f' readonly value='" + f + "'></td>" +

                            "<td><input type='number' class='form-control total' readonly value='" + total + "'></td>" +

                            "</tr>"
                        );
                    }
                }

                // =========================================
                // NULL LOGIC
                // =========================================

                if (TOTAL_TON_SC_S === 0)
                    TOTAL_TON_SC_S = "";

                if (TOTAL_TON_NC_H === 0)
                    TOTAL_TON_NC_H = "";

                if (TOTAL_TON_NC_BF_KO === 0)
                    TOTAL_TON_NC_BF_KO = "";

                if (TOTAL_TON_NC_P25 === 0)
                    TOTAL_TON_NC_P25 = "";

                // =========================================
                // DISPLAY TOTALS
                // =========================================

                //$("#TOTAL_TON_SC_S").val(TOTAL_TON_SC_S);

                //$("#TOTAL_TON_NC_H").val(TOTAL_TON_NC_H);

                //$("#TOTAL_TON_NC_BF_KO").val(TOTAL_TON_NC_BF_KO);

                //$("#TOTAL_TON_NC_P25").val(TOTAL_TON_NC_P25);
            }
        });
    }

</script>
<script>
function loadUsers() {
 $.ajax({
     url: '/Furnace_High_line/GetUsers',
     type: 'GET',
        success: function (data) {
        var dl = document.getElementById("UserList"); 
        dl.innerHTML = ""; 
        for (var i = 0; i < data.length; i++) {
            var option = document.createElement("option");
            option.value = data[i].USER_NAME;
            dl.appendChild(option);
        }
        },
    error: function () {
    alert("Data Load Error");
    }
});
}
function signoff() {
    var obj = {
        NAME: $("#txtUser").val(),
        SO_DATE: $("#currDate-value").val(),
        SO_SHIFT: $("#ddlshift").val(),
        SO_CHECK: $("#signoff").is(":checked") ? 1 : 0
    };

    $.ajax({
        url: '/Furnace_High_line/SaveSignOff',
        type: 'POST',
        data: obj,
        success: function (res) {                       
            if (obj.SO_CHECK == 1) {
                $("#CokeUnloading").prop("disabled", true);                
            }
            else {
                $("#CokeUnloading").prop("disabled", false);                
            }
        },

        error: function () {
            alert("Error");
        }
    });
}
function loadShiftData() {
    debugger;
    var sDate = $("#currDate-value").val();
    var sShift = $("#ddlshift").val();
    if (sDate == "" || sShift == "") {
        return;
    }
    $.ajax({
        url: '/Furnace_High_line/GetShiftData',
        type: 'GET',
        data: {
            debugger;
            sDate: sDate,
            sShift: sShift
        },
        success: function (res) {
            if (res.success == true) {                
                $("#txtUser").val(res.SIGNOFF_NAME);
                if (res.SO_CHECK == 1) {
                    $("#signoff").prop("checked", true);                    
                    $("#CokeUnloading").prop("disabled", true);                    
                }
                else {
                    $("#signoff").prop("checked", false);
                    $("#CokeUnloading").prop("disabled", false);                    
                }             
                Display_Bin_Position();
                copyDateShiftToRows();  
                Display_Coke_unloading();  
                LoadTonnageFromDB();
                TotUL();         
            }

        },

        error: function () {

            alert("Error Loading Data");

        }

    });

}
</script>
</body>
</html>
