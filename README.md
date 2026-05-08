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
                                <div style="margin-left:100px;margin-top:100px;">
                                    <button class="btn btn-success" onclick="SaveCokeUnloading()">
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
                <button class="btn btn-success" style="margin-left:500px;margin-top:10px;" onclick="SaveFurnaceBinPosition()">
                    💾 Save
                </button>
            </div>

        </div>    
        <!-- Loader -->
        <div class="loader-container" id="loaderDiv">
            <div class="loader"></div>
        </div>
     </div>   
