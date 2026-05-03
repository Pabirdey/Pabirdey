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
   
    </style>

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
                                    <table class="table table-bordered text-center">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody id="tblBodyCoke"></tbody>
                                    </table>
                                </div>
                            </div>
                            <!-- Tonnage of Nut Coke -->
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                    <div class="section-title">Tonnage of Nut Coke</div>
                                    <table class="table table-bordered text-center">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody id="tblBodyNutCoke"></tbody>
                                    </table>
                                </div>
                            </div>
                        </div>                                            
                    </div>
                   
                    
                     <div class="col-md-4">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="section-box">
                                    <h6>Others</h6>
                                    <input class="form-control mb-2" placeholder="Stock Coke Eastern Bunker">
                                    <input class="form-control mb-2" placeholder="Stock Coke Western Bunker">
                                    <input class="form-control mb-2" placeholder="Behive Coke in Middle Bunker">
                                </div>
                                <div class="section-box mt-2">
                                    <h6>Remarks & Delays</h6>
                                    <textarea class="form-control cell" style="height:150px;" data-id="R246"></textarea>
                                </div>

                            </div>
                            <div class="col-md-6">
                                <div class="section-box">
                                    <h6>Coke & Nut Coke Advised & Received</h6>
                                    <input class="form-control mb-2 cell" data-id="R50" placeholder="Material advised">
                                    <input class="form-control mb-2 cell" data-id="R51" placeholder="Time advised">
                                    <input class="form-control mb-2 cell" data-id="R52" placeholder="Material received">
                                    <input class="form-control mb-2 cell" data-id="R53" placeholder="Time received">
                                    <input class="form-control mb-2 cell" data-id="R54" placeholder="Unloaded">
                                    <input class="form-control mb-2 cell" data-id="R55" placeholder="Loco left">
                                    <input class="form-control mb-2 cell" data-id="R56" placeholder="Sent down">
                                    <input class="form-control mb-2 cell" data-id="R57" placeholder="Total">
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
                                        <th style="width:5px;">Material</th>
                                        <th style="width:15px;">Recd.</th>
                                        <th style="width:20px;">Retd.</th>
                                        <th style="width:120px;">Reason</th>
                                        <th style="width:20px;">U/L</th>
                                        <th style="width:20px;">Balance</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td class="text-start ps-1">LRP(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R58"></td>
                                        <td><input type="text" class="form-control cell" data-id="R59"></td>
                                        <td><input type="text" class="form-control cell" data-id="R60"></td>
                                        <td><input type="text" class="form-control cell" data-id="R61"></td>
                                        <td><input type="text" class="form-control cell" data-id="R62"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">LRP(IN)</td>
                                        <td><input type="text" class="form-control cell" data-id="R63"></td>
                                        <td><input type="text" class="form-control cell" data-id="R64"></td>
                                        <td><input type="text" class="form-control cell" data-id="R65"></td>
                                        <td><input type="text" class="form-control cell" data-id="R66"></td>
                                        <td><input type="text" class="form-control cell" data-id="R67"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">JODA(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R68"></td>
                                        <td><input type="text" class="form-control cell" data-id="R69"></td>
                                        <td><input type="text" class="form-control cell" data-id="R70"></td>
                                        <td><input type="text" class="form-control cell" data-id="R71"></td>
                                        <td><input type="text" class="form-control cell" data-id="R72"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">JODA(IN)</td>
                                        <td><input type="text" class="form-control cell" data-id="R73"></td>
                                        <td><input type="text" class="form-control cell" data-id="R74"></td>
                                        <td><input type="text" class="form-control cell" data-id="R75"></td>
                                        <td><input type="text" class="form-control cell" data-id="R76"></td>
                                        <td><input type="text" class="form-control cell" data-id="R77"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">TFO</td>
                                        <td><input type="text" class="form-control cell" data-id="R78"></td>
                                        <td><input type="text" class="form-control cell" data-id="R79"></td>
                                        <td><input type="text" class="form-control cell" data-id="R80"></td>
                                        <td><input type="text" class="form-control cell" data-id="R81"></td>
                                        <td><input type="text" class="form-control cell" data-id="R82"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">PELLET</td>
                                        <td><input type="text" class="form-control cell" data-id="R351"></td>
                                        <td><input type="text" class="form-control cell" data-id="R352"></td>
                                        <td><input type="text" class="form-control cell" data-id="R353"></td>
                                        <td><input type="text" class="form-control cell" data-id="R354"></td>
                                        <td><input type="text" class="form-control cell" data-id="R355"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">SCRAP</td>
                                        <td><input type="text" class="form-control cell" data-id="R88"></td>
                                        <td><input type="text" class="form-control cell" data-id="R89"></td>
                                        <td><input type="text" class="form-control cell" data-id="R90"></td>
                                        <td><input type="text" class="form-control cell" data-id="R91"></td>
                                        <td><input type="text" class="form-control cell" data-id="R92"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">L/STONE</td>
                                        <td><input type="text" class="form-control cell" data-id="R93"></td>
                                        <td><input type="text" class="form-control cell" data-id="R94"></td>
                                        <td><input type="text" class="form-control cell" data-id="R95"></td>
                                        <td><input type="text" class="form-control cell" data-id="R96"></td>
                                        <td><input type="text" class="form-control cell" data-id="R97"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">PYROXINITE</td>
                                        <td><input type="text" class="form-control cell" data-id="R98"></td>
                                        <td><input type="text" class="form-control cell" data-id="R99"></td>
                                        <td><input type="text" class="form-control cell" data-id="R100"></td>
                                        <td><input type="text" class="form-control cell" data-id="R101"></td>
                                        <td><input type="text" class="form-control cell" data-id="R102"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">QUARTZ</td>
                                        <td><input type="text" class="form-control cell" data-id="R103"></td>
                                        <td><input type="text" class="form-control cell" data-id="R104"></td>
                                        <td><input type="text" class="form-control cell" data-id="R105"></td>
                                        <td><input type="text" class="form-control cell" data-id="R106"></td>
                                        <td><input type="text" class="form-control cell" data-id="R107"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">NUT COKE</td>
                                        <td><input type="text" class="form-control cell" data-id="R108"></td>
                                        <td><input type="text" class="form-control cell" data-id="R109"></td>
                                        <td><input type="text" class="form-control cell" data-id="R110"></td>
                                        <td><input type="text" class="form-control cell" data-id="R111"></td>
                                        <td><input type="text" class="form-control cell" data-id="R112"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">STOCK SINTER</td>
                                        <td><input type="text" class="form-control cell" data-id="R113"></td>
                                        <td><input type="text" class="form-control cell" data-id="R114"></td>
                                        <td><input type="text" class="form-control cell" data-id="R115"></td>
                                        <td><input type="text" class="form-control cell" data-id="R116"></td>
                                        <td><input type="text" class="form-control cell" data-id="R117"></td>
                                    </tr>
                                    <tr>
                                        <td class="text-start ps-1">SINTER(FLB)</td>
                                        <td><input type="text" class="form-control cell" data-id="R271"></td>
                                        <td><input type="text" class="form-control cell" data-id="R272"></td>
                                        <td><input type="text" class="form-control cell" data-id="R273"></td>
                                        <td><input type="text" class="form-control cell" data-id="R274"></td>
                                        <td><input type="text" class="form-control cell" data-id="R275"></td>
                                    </tr>
                                </tbody>
                            </table>

                            <div class="text-end">
                                <strong>Total: 35 / 7</strong>
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
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                    </tr>
                                    <tr>
                                        <td>SP2</td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
                                        <td><input type="text" class="form-control cell" data-id=""></td>
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
                                    <input type="text" class="form-control cell" data-id="R301" style="width:80px;">
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
                       <button class="btn btn-success" onclick="SaveHighLine()">
                                💾 Save
                        </button>            
                    </div>              
                </div>
            </div>
            <!-- TAB 3 -->
            <div class="tab-pane fade" id="tab3">
                <div class="container mt-4">
                    <div class="card-custom" style="width:1100px;">
                        <div class="mb-3 position-relative">                            
                            <h4 class="text-center m-0 fw-bold" style="font-size:22px;">
                                Raw Material Position
                            </h4>                            
                            <button class="btn btn-success px-4 position-absolute end-0 top-50 translate-middle-y"
                                    onclick="SaveBinPosition()">
                                💾 Save
                            </button>
                        </div>
                        <div class="table-container">
                            <table class="table table-bordered table-custom">
                                <thead class="font-size:12px;">
                                    <tr>
                                        <th>Material</th>
                                        <th>Yard Position</th>
                                        <th>H.L.Position</th>
                                        <th>Stock Loaded</th>
                                        <th>C-BF</th>
                                        <th>E-BF</th>
                                        <th>F-BF</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td class="material-name">Sinter</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R147"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R148"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R149"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R152"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R154"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R155"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">TFO</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R156"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R157"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R158"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R161"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R163"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R164"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">LRP</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R165"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R166"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R167"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R170"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R172"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R173"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Joda</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R174"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R175"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R176"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R179"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R181"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R182"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Pellet</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R383"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R384"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R385"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R388"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R390"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R391"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Nut Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R192"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R193"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R194"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R197"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R199"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R200"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Limestone</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R201"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R202"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R203"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R206"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R208"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R209"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Pyroxinite</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R210"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R211"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R212"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R215"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R217"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R218"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">ORT</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R219"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R220"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R221"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R224"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R226"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R227"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Scrap</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R228"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R229"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R230"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R233"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R235"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R236"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Coke(On Stock)</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R237"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R238"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R239"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R242"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R244"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R245"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">Low Ash Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R307"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R308"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R309"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R312"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R314"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R315"></td>
                                    </tr>
                                    <tr>
                                        <td class="material-name">High Ash Coke</td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R316"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R317"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R318"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R321"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R323"></td>
                                        <td><input type="text" class="form-control cell text-start ps-0" data-id="R324"></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>

                    </div>
                </div>

            </div>

        </div>
    </div>
    <script src="~/js/Jquey3.6.0.min.js"></script>
    <script src="~/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/bootstrap-datepicker.min.js"></script>
    <script>
        let lsSelectedFDate;        
        $(document).ready(function () {
            lsSelectedFDate = '@DateTime.Today.AddDays(0).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
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
                Display_Bin_Position();
                copyDateShiftToRows();
            });
            $('#ddlshift').on('change', function () {
                Display_Bin_Position();
                copyDateShiftToRows();
            });
            Display_Bin_Position();
            copyDateShiftToRows();            

           
        });
    </script>
   <script>
       function copyDateShiftToRows() {
           // Get header values
           var headerDate = document.getElementById("hiddenDate").value;
           var headerShift = document.getElementById("ddlshift").value;
           // Loop all rows
           document.querySelectorAll("#tblBody tr").forEach(function (row) {
               var dateInput = row.querySelector(".row-date");
               var shiftSelect = row.querySelector(".row-shift");
               if (dateInput) dateInput.value = headerDate;
               if (shiftSelect) shiftSelect.value = headerShift;

           });
       }
       function Display_Coke_Unloading() {
           var shift = $("#ddlshift").val();

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

       
       function SaveBinPosition() {
           var list = [];
           var shift = $("#ddlshift").val();
           $(".cell").each(function () {
               //var value = $(this).val();
               //var cellId=$(this).data("id");
               //if(value!==null && value.trim()!==""){
               list.push({
                   CellId: $(this).data("id"),
                   Value: $(this).val(),
                   Date: lsSelectedFDate,
                   Shift: shift
               });
            //}
           });

           console.log(list);
           $.ajax({
               url: '/Furnace_High_line/Save_Furnace_High_Line',
               type: 'POST',
               data: JSON.stringify({ list: list }),  
               contentType: 'application/json',
               success: function (res) {
                   if (res.success) {
                       alert(res.message);   
                   }
                   else {
                       alert(res.message);
                   }
               },

               error: function () {
                   alert("Save failed!");
               }
           });
       }
       

   </script>
    <script>
        function createRow(item = {}) {
        return `
        <tr>
            <td>
                <input type="text" class="form-control row-date" style="width:100px;"
                value="${formatDate(item.TIMESTAMP)}" readonly>
            </td>

            <td>
                <select class="form-control row-shift">
                    <option ${item.SHIFT == 'A' ? 'selected' : ''}>A</option>
                    <option ${item.SHIFT == 'B' ? 'selected' : ''}>B</option>
                    <option ${item.SHIFT == 'C' ? 'selected' : ''}>C</option>
                </select>
            </td>

            <td>
                <select class="form-control bunker" style="width:200px;">
                    <option value="">---Pls. Select---</option>
                    <option ${item.BUNKER=='WESTERN'?'selected':''}>WESTERN</option>
                    <option ${item.BUNKER=='MIDDLE'?'selected':''}>MIDDLE</option>
                    <option ${item.BUNKER=='EASTERN'?'selected':''}>EASTERN</option>
                    <option ${item.BUNKER=='H/S NC'?'selected':''}>H/S NC</option>
                    <option ${item.BUNKER=='NC BF KO'?'selected':''}>NC BF KO</option>
                    <option ${item.BUNKER=='ST.COKE-HALDIA'?'selected':''}>ST.COKE-HALDIA</option>
                    <option ${item.BUNKER=='ST.COKE-IMPORTED'?'selected':''}>ST.COKE-IMPORTED</option>
                    <option ${item.BUNKER=='ST.COKE-OWN'?'selected':''}>ST.COKE-OWN</option>
                    <option ${item.BUNKER=='ST.COKE-TOTAL'?'selected':''}>ST.COKE-TOTAL</option>
                    <option ${item.BUNKER=='B/H HIGH ASH'?'selected':''}>B/H HIGH ASH</option>
                    <option ${item.BUNKER=='B/H LOW ASH'?'selected':''}>B/H LOW ASH</option>
                    <option ${item.BUNKER=='B/H COKE-TOTAL'?'selected':''}>B/H COKE-TOTAL</option>
                    <option ${item.BUNKER=='ROUGH BREEZE'?'selected':''}>ROUGH BREEZE</option>
                    <option ${item.BUNKER=='PLS_25MM_NC'?'selected':''}>PLS_25MM_NC</option>
                </select>
            </td>

            <td><input type="text" class="form-control val c" value="${item.C || ''}"></td>
            <td><input type="text" class="form-control val e" value="${item.E || ''}"></td>
            <td><input type="text" class="form-control val f" value="${item.F || ''}"></td>

            <td><input type="text" class="form-control total" value="${item.TOTAL || ''}" readonly></td>

            <td><input type="text" class="form-control position" value="${item.BUNKER_P || ''}"></td>
            <td><input type="text" class="form-control balance" value="${item.BALANCE || ''}"></td>
        </tr>`;
                }


    </script>
</body>
</html>
