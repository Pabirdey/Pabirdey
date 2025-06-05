@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Quantity</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .form-label {
            font-weight: 600;
            font-family:Georgia;            
        }

        .section-divider {
            border-top: 2px solid #bbb;
            margin-top: 20px;
            margin-bottom: 20px;
            border-color:blueviolet;            
        }

        .material-row .form-label {
            padding-top: 0.375rem;
        }

        .material-row .col-md-2 {
            display: flex;
            align-items: center;
        }

        .material-row .form-control {
            /*flex: 1;*/
            width:160px;
        }

        .material-row label {
            min-width: 130px;
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4" style="font-family:'Comic Sans MS';text-align:center;font-weight:800;">Raw Material Quantity</h4>
        <hr class="section-divider">
        <form>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Pile No</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Source</label>
                    <select class="form-control-sm">
                        <option value="RMBB_KNR">RMBB_KNR</option>
                        <option value="RMBB">RMBB</option>
                        <option value="RMBBN">RMBBN</option>

                    </select>
                </div>
                <div class="col-md-2">
                    <label class="form-label">Shift</label>
                    <select class="form-control-sm">
                        <option value="A">A</option>
                        <option value="B">B</option>
                        <option value="C">C</option>

                    </select>                    
                </div>
                <div class="col-md-2">
                    <label class="form-label">Start Date</label>
                   <input type="datetime-local" />
                </div>
                <div class="col-md-2">
                    <label class="form-label">End Date</label>
                    <input type="date" />
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cons.St.Date</label>
                    <input type="date" />
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <!-- Third row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coastal Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Deobhar/Katamati Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual S/O(Lump)</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">FSF Venezuelan</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">SN Feed Value</label>
                    <input class="form-control" type="text">
                </div>

            </div>
            <!-- Fourth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Other Imp Ore</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Imp Ore Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bacheli</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jaroli</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kay Pee Entp</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Diatari</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <!-- Fifth row of materials -->
            <div class="row material-row mb-2">               
                <div class="col-md-2">
                    <label class="form-label">Domestic IOF</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Iron Ore Fines</label>
                    <input class="form-control" type="text">
                </div>

            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone HI Silica</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone RPD</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone SP Grade</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag(O/S)</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soap Stone</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone Gotan</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone Stone(Imported)</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone Himachal</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bhutan Dolo</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Gomardih Dolo</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone (Phillipines)</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite(Local)</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Mixed Flux</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">LD Sludge</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Mill Scale</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Kiln Dust</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label">Solid Waste</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" >
                </div>
                </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Mill Sludge</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Flue Dust</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Esp Dust</label>
                    <input class="form-control" type="text" readonly>
                </div>                
                <div class="col-md-1">                    
                </div>                
                <div class="col-md-2">
                </div>                
                <div class="col-md-1">
                    <button type="button" class="btn btn-warning">OK</button>
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">GCP Sludge</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Fresh</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Lime Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag Fines</label>
                    <input class="form-control" type="text">
                </div>                                             
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">WRP</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Dolo Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Flue Dust</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Sludge</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">ESP Dust</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Revert Material</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Mix</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soild Mix</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Scale</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kiln Dust</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Coke Breeze</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">RPC</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Jhama Coal</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label">G Sinter Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pellet SN Fines</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">G ORE Fines</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM(End Cone)</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Anthracite</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM Previous</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Mixed Material</label>
                    <input class="form-control" type="text" readonly>
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text">
                </div>   
                <div class="col-md-2">
                    <label class="form-label"style="color:#ff6a00">Total Pile</label>
                    <input class="form-control" type="text" readonly>
                </div>
                <div class="col-md-2">
                    <label class="form-label">No Of Layers</label>
                    <input class="form-control" type="text">
                </div>             
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text">
                </div>  
                <div class="col-md-2">
                    <button type="button" class="btn btn-success">Add</button>
                    <button type="button" class="btn btn-success">Save</button>
                    <button type="button" class="btn btn-info">Exit</button>
                </div>                 
            </div>

            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text">
                </div>
            </div>
</form>
    </div>
</body>
</html>
