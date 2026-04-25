<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Sofia">

    <style>
        body { background: #f4f6f9;font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;font-weight: bold; }

        .header-box {
            background: #0d47a1;
            color: white;
            padding: 10px;
            border-radius: 10px;
        }

        .section-box {
            background: #1976d2;
            color: white;
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
        }

        .table input { width: 60px; }
        textarea { height: 120px; }

        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 10px;
            color: white;
        }

        .table-custom {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
        }

        .table-custom th {
            background-color: #1565c0;
            color: white;
            text-align: center;
        }

        .table-custom td {
            text-align: center;
            padding: 6px;
        }

        .material-name {
            font-weight: bold;
            background-color: #e3f2fd;
        }

        .btn-custom {
            width: 120px;
            border-radius: 25px;
        }

        .table-container {
            max-height: 800px;
            overflow-y: auto;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">
    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4 class="m-0" style="font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;">Furnace High Line Log Sheet</h4>
        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </div>
    </div>
    <!-- TABS -->
    <ul class="nav nav-tabs mt-3">
        <li class="nav-item">
            <a class="nav-link active" data-bs-toggle="tab" href="#tab1" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:20px;">Coke Unloading</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab2" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:20px;">HighLine Log</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab3" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:20px;">Bin Position</a>
        </li>
    </ul>

    <!-- TAB CONTENT -->
    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">

            <div class="row mt-2">

                <!-- LEFT TABLE -->
                <div class="col-md-8">
                    <div class="section-box">
                        <h6>Coke Unloading</h6>

                        <div class="table-responsive">
                            <table class="table table-bordered text-center bg-white">
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
                    </div>
                </div>

                <!-- RIGHT SIDE -->
                <div class="col-md-4">

                    <div class="row">

                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Others</h6>
                                <input class="form-control mb-2" placeholder="Eastern Bunker">
                                <input class="form-control mb-2" placeholder="Western Bunker">
                                <input class="form-control mb-2" placeholder="Middle Bunker">
                            </div>
                        </div>

                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Coke & Nut Coke</h6>
                                <input class="form-control mb-2" placeholder="Material advised">
                                <input class="form-control mb-2" placeholder="Time advised">
                                <input class="form-control mb-2" placeholder="Material received">
                                <input class="form-control mb-2" placeholder="Time received">
                                <input class="form-control mb-2" placeholder="Unloaded">
                                <input class="form-control mb-2" placeholder="Loco left">
                                <input class="form-control mb-2" placeholder="Sent down">
                                <input class="form-control mb-2" placeholder="Total">
                            </div>
                        </div>

                    </div>
                    <div class="section-box mt-2">
                        <h6>Remarks & Delays</h6>
                        <textarea class="form-control"></textarea>
                    </div>
                </div>
            </div>
        </div>
        <div class="tab-pane fade show active" id="tab2">
            <div class="row mt-2">            
                 
        <!-- LEFT PANEL -->
        <div class="col-md-7">
            <div class="section-box">
                <div class="section-title">High Line Log</div>
                <table class="table table-bordered text-center bg-white text-dark">
                    <thead>
                        <tr>
                            <th style="width:20px;">Material</th>
                            <th style="width:15px;">Recd.</th>
                            <th style="width:20px;">Retd.</th>
                            <th style="width:100px;">Reason</th>
                            <th style="width:20px;">U/L</th>
                            <th style="width:20px;">Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>LRP(FLB)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>LRP(IN)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>JODA(FLB)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>JODA(IN)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>TFO</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>PELLET</td>
                             <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SCRAP</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>L/STONE</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>Pyroxinite</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>Quartz</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>Nut Coke</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>Stock Sinter</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>Sinter(FLB)</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
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
        <div class="col-md-2">
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
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SP2</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
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
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SP2</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
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
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SP2</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
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
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>SP1</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                        <tr>
                            <td>SP2</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>
            </div>                               
        </div>

        <!-- RIGHT PANEL -->
        <div class="col-md-3">

            <div class="section-box">
                <div class="section-title">Sinter Storage</div>
                <label>SP1<input type="text"></label>
                <label>SP2<input type="text"></label>
                <label>Total Fines(t)<input type="text"></label>
                <label>SP1 Fines(%)<input type="text"></label>
                <label>SP2 Fines(%)<input type="text"></label>
            </div>

            <div class="section-box">
                <div class="section-title">Reclaimed Ore</div>
                <label>LRP<input class="form-control"></label>
                <label>Direct Fines<input class="form-control"></label>
                <label>Reclaimed Fines<input class="form-control"></label>
                <label>JODA<input class="form-control"></label>
                <label>Direct Fines<input class="form-control"></label>
                <label>Reclaimed Fines<input class="form-control"></label>
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
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                    <tr>
                        <td>2</td>
                        <td>                            
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                    <tr>
                        <td>3</td>
                        <td>                            
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                    <tr>
                        <td>4</td>
                        <td>                            
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                    <tr>
                        <td>5</td>
                        <td>                            
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                    <tr>
                        <td>6</td>
                        <td>                            
                            <select class="form-select">
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
                        <td><input class="form-control"></td>
                    </tr>
                </table>
            </div>      
            <div class="text-center mt-3">
                <button class="btn btn-success btn-custom">Save</button>                
                <button class="btn btn-secondary btn-custom">Exit</button>
            </div>   
        </div>

    </div>                                  
 </div>
        </div>

        <!-- TAB 3 -->
        <div class="tab-pane fade" id="tab3">
            <div class="container mt-4">
                <div class="card-custom">
                    <h4 class="text-center mb-4" style="font-size:32px;">Raw Material Position</h4>
                    <div class="table-container">
                        <table class="table table-bordered table-custom">
                            <thead>
                                <tr>
                                    <th style="width:20px;height:10px">Material</th>
                                    <th style="width:20px;height:10px">Yard Position</th>
                                    <th style="width:20px;height:10px">H.L. Position</th>
                                    <th style="width:20px;height:10px";>Stock Loaded</th>
                                    <th style="width:20px;height:10px";>C-BF</th>
                                    <th style="width:20px;height:10px";>E-BF</th>
                                    <th style="width:20px;height:10px";>F-BF</th>                                    
                                </tr>
                            </thead>

                            <tbody>
                                <tr>
                                    <td class="material-name">SINTER</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>                            
                                <tr>
                                    <td class="material-name">TFO</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                                <tr>
                                    <td class="material-name">LRP</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                            <tr>
                                <td class="material-name">JODA</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Pellet</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Nut Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Limestone</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Pyroxinite</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">ORT</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Scrap</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                               <td class="material-name">Coke(On Stock)</td> 
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Low Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">High Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                        </tbody>
                        </table>
                    </div>

                </div>

            </div>

        </div>

    </div>

</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>
function createRow() {
    return `
    <tr>
        <td><input type="date" class="form-control"></td>
        <td>
            <select class="form-control">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>
        <td><input class="form-control"></td>
        <td><input class="form-control c" oninput="calcTotal(this)"></td>
        <td><input class="form-control e" oninput="calcTotal(this)"></td>
        <td><input class="form-control f" oninput="calcTotal(this)"></td>
        <td><input class="form-control total" readonly></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
    </tr>`;
}

function calcTotal(el) {
    var row = el.closest("tr");

    var c = parseFloat(row.querySelector(".c").value) || 0;
    var e = parseFloat(row.querySelector(".e").value) || 0;
    var f = parseFloat(row.querySelector(".f").value) || 0;

    row.querySelector(".total").value = c + e + f;
}

// generate rows
for (let i = 0; i < 5; i++) {
    document.getElementById("tblBody").innerHTML += createRow();
}
</script>

</body>
</html>
