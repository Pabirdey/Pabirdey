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
            font-family: Georgia;
        }

        .section-divider {
            border: 3px solid #8e2626;
            width: 100%;
            margin: 20px auto;        
        }

        .material-row .form-label {
            padding-top: 0.375rem;
        }

        .material-row .col-md-2 {
            display: flex;
            align-items: center;
        }

        .material-row .form-control {
            width: 150px;
        }

        .material-row label {
            min-width: 140px;
            margin-right: 10px;
        }
        h6{
            font-family:Georgia, 'Times New Roman', Times, serif;
            font-weight:bold;
            color:#8e2626;
        }
        
    </style>
</head>
<body>
    <div class="container-fluid mt-4">
        <h4 class="mb-4" style="font-family:'Comic Sans MS';text-align:center;font-weight:bold;color:#4CAF50;font-size:xx-large;">Raw Material Quantity</h4>
        <hr class="section-divider">
        <form method="post" action="/Blast_Furnace/RawMaterialEntry" id="rawMaterialForm">
            <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input class="form-control" type="text" value="@Model.PileNo" name="PileNo" placeholder="Enter PileNo" autocomplete="off">
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Select Source</label>
                        <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model !=null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>

                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>iro
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="datetime-local" class="form-control" name="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="datetime-local" class="form-control" name="EndDate" value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="datetime-local" class="form-control" name="ConsStartDate" value="@(Model.ConsStartDate.HasValue ? Model.ConsStartDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NoaFines" name="NoaFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JodaFines" name="JodaFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KBFines" name="KBFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YardFines" name="YardFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.BHJ" name="BHJ" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.Namisa" name="Namisa" autocomplete="off">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text" value="@Model.FortescueBF" name="FortescueBF" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text" value="@Model.NoaCrushed" name="NoaCrushed" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text" value="@Model.JoaCrushed" name="JoaCrushed" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text" value="@Model.KbCrushed" name="KbCrushed" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text" name="Pilbhara" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text" value="@Model.Kumba" name="Kumba" autocomplete="off">
                </div>
            </div>
            <!-- Third row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coastal Fines</label>
                    <input class="form-control" type="text" value="@Model.CoastalFines" name="CoastalFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Deobhar/ Katamati Fines</label>
                    <input class="form-control" type="text" value="@Model.KatamatiFines" name="KatamatiFines" style="margin:4px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual S/O(Lump)</label>
                    <input class="form-control" type="text" value="@Model.KirandulLump" name="KirandulLump" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual Fines</label>
                    <input class="form-control" type="text" value="@Model.KirandulLump" name="KirandulLump" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">FSF Venezuelan</label>
                    <input class="form-control" type="text" value="@Model.FSFVenezuelan" name="FSFVenezuelan" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">SN Feed Value</label>
                    <input class="form-control" type="text" value="@Model.SnFeedValue" name="SnFeedValue" autocomplete="off">
                </div>

            </div>
            <!-- Fourth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Other Imp Ore</label>
                    <input class="form-control" type="text" value="@Model.OtherImpOre" name="OtherImpOre" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Imp Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.ImpOreFines" name="ImpOreFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bacheli</label>
                    <input class="form-control" type="text" value="@Model.Bacheli" name="Bacheli" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jaroli</label>
                    <input class="form-control" type="text" value="@Model.Jaroli" name="Jaroli" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kay Pee Entp</label>
                    <input class="form-control" type="text" value="@Model.KayPeeEntp" name="KayPeeEntp" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Diatari</label>
                    <input class="form-control" type="text" value="@Model.Daitari" name="Daitari" autocomplete="off">
                </div>
            </div>
            <!-- Fifth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Domestic IOF</label>
                    <input class="form-control" type="text" value="@Model.DomesticIOF" name="DomesticIOF" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Iron Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.IronOreFines" name="IronOreFines" autocomplete="off">
                </div>

            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone HI Silica</label>
                    <input class="form-control" type="text" value="@Model.LimestoneHISilica" name="LimestoneHISilica" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone RPD</label>
                    <input class="form-control" type="text" value="@Model.LimestoneRPD" name="LimestoneRPD" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone SP Grade</label>
                    <input class="form-control" type="text" value="@Model.LimestoneSPGrade" name="LimestoneSPGrade" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag(O/S)</label>
                    <input class="form-control" type="text" value="@Model.LDSlagOs" name="LDSlagOs" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soap Stone</label>
                    <input class="form-control" type="text" value="@Model.SoapStone" name="SoapStone" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone Gotan</label>
                    <input class="form-control" type="text" value="@Model.LimestoneGotan" name="LimestoneGotan" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone Stone(Imported)</label>
                    <input class="form-control" type="text" value="@Model.LimestoneImp" name="LimestoneImp" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone Himachal</label>
                    <input class="form-control" type="text" value="@Model.LimestoneHimachal" name="LimestoneHimachal" style="margin:4px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bhutan Dolo</label>
                    <input class="form-control" type="text" value="@Model.BhutanDolo" name="BhutanDolo" style="margin:8px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Gomardih Dolo</label>
                    <input class="form-control" type="text" value="@Model.GomardihDolo" name="GomardihDolo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone (Phillipines)</label>
                    <input class="form-control" type="text" value="@Model.LimestonePhilipines" name="LimestonePhilipines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite(Local)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteLocal" name="PyroxeniteLocal" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite (Sukinda)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteSukinda" name="PyroxeniteSukinda" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite  (Imp)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteImp" name="PyroxeniteImp" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone(CP Gr.)</label>
                    <input class="form-control" type="text" value="@Model.LimestoneCPGr" name="LimestoneCPGr" style="margin:8px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Olivine</label>
                    <input class="form-control" type="text" value="@Model.Olivine" name="Olivine" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Flux</label>
                    <input class="form-control" type="text" readonly value="@Model.MixedFlux" name="MixedFlux" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">LD Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.LdSludge" name="LdSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Scale</label>
                    <input class="form-control" type="text" readonly value="@Model.MillScale1" name="MillScale1" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Kiln Dust</label> 
                    <input class="form-control" type="text" readonly value="@Model.Kilndust" name="Kilndust" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Solid Waste</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" value="@Model.SolidWaste" name="SolidWaste" autocomplete="off">
                </div>                
                    <div class="col-md-2">
                        <label class="form-label">PSW1</label>
                        <input class="form-control" type="text" value="@Model.PSw1" name="PSw1" autocomplete="off">
                    </div>                
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.MillSludge" name="MillSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Flue Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.Fluedust" name="Fluedust" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Esp Dust</label> 
                    <input class="form-control" type="text" readonly value="@Model.ESPdust" name="ESPdust" autocomplete="off">
                </div>
                <div class="col-md-1">
                </div>
                <div class="col-md-2">
                </div>
                <div class="col-md-1">
                    <button type="button" class="btn btn-warning">OK</button>
                </div>
                <div class="col-md-2">
                    <label class="form-label">PSW2</label>
                    <input class="form-control" type="text" value="@Model.PSW2" name="PSW2" autocomplete="off">
                </div>   
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">GCP Sludge</label>
                    <input class="form-control" type="text" value="@Model.GCPSludge" name="GCPSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Fresh</label>
                    <input class="form-control" type="text" value="@Model.LDSludgeFresh" name="LDSludgeFresh" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Lime Fines</label>
                    <input class="form-control" type="text" value="@Model.LimeFines" name="LimeFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag Fines</label>
                    <input class="form-control" type="text" value="@Model.LDSlagFines" name="LDSlagFines" autocomplete="off">
                </div>
                <div class="col-md-2">                   
                </div>
                <div class="col-md-2">
                    <label class="form-label">Blend-I</label>
                    <select id="LstBlend">
                    </select>
                </div>   
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">WRP</label>
                    <input class="form-control" type="text" value="@Model.WRP" name="WRP" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Dolo Fines</label>
                    <input class="form-control" type="text" value="@Model.DoloFines" name="DoloFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Flue Dust</label>
                    <input class="form-control" type="text" value="@Model.Fludust" name="Fludust" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Sludge</label>
                    <input class="form-control" type="text" value="@Model.MillSludge1" name="MillSludge1" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">ESP Dust</label>
                    <input class="form-control" type="text" value="@Model.ESPDust2" name="ESPDust2" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Blend-II</label>
                    <select id="LstBlend"></select>
                </div>  
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Revert Material</label>
                    <input class="form-control" type="text" readonly value="@Model.RevertMat" name="RevertMat" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Mix</label>
                    <input class="form-control" type="text" value="@Model.LDSludgeMix" name="LDSludgeMix" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soild Mix</label>
                    <input class="form-control" type="text" value="@Model.SolidMix" name="SolidMix" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Scale</label>
                    <input class="form-control" type="text" value="@Model.MIllScale" name="MIllScale" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kiln Dust</label>
                    <input class="form-control" type="text" value="@Model.KilnDust1" name="KilnDust1" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Coke Breeze</label>
                    <input class="form-control" type="text" readonly value="@Model.CokeBreeze" name="CokeBreeze" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">RPC</label>
                    <input class="form-control" type="text" readonly value="@Model.RPC" name="RPC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Jhama Coal</label>
                    <input class="form-control" type="text" readonly value="@Model.JhamaCoal" name="JhamaCoal" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">G Sinter Fines</label>
                    <input class="form-control" type="text" value="@Model.GSinterFines" name="GSinterFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pellet SN Fines</label>
                    <input class="form-control" type="text" value="@Model.PelletSNFines" name="PelletSNFines" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">G ORE Fines</label>
                    <input class="form-control" type="text" value="@Model.GOreFines" name="GOreFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM(End Cone)</label>
                    <input class="form-control" type="text" value="@Model.BMEndCone" name="BMEndCone" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Anthracite</label>
                    <input class="form-control" type="text" value="@Model.Anthracite" name="Anthracite" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM Previous</label>
                    <input class="form-control" type="text" value="@Model.BMPrevious" name="BMPrevious" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Material</label>
                    <input class="form-control" type="text" readonly value="@Model.MixedMaterial" name="MixedMaterial" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.PileChemSio2" name="PileChemSio2" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.PileChemCao" name="PileChemCao" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.PileChemPhos" name="PileChemPhos" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.PileChemAl2O3" name="PileChemAl2O3" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Total Pile</label>
                    <input class="form-control" type="text" readonly value="@Model.TotalPile" name="TotalPile" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">No Of Layers</label> 
                    <input class="form-control" type="text" value="@Model.NoOfLayer" name="NoOfLayer" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">               
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.PileChemMgo" name="PileChemMgo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.PileChemC" name="PileChemC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.PileChemOil" name="PileChemOil" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.PileChemFeo" name="PileChemFeo" autocomplete="off">
                </div>
                <div class="col-md-2">                                        
                    <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary"/>                    
                </div>
            </div>

            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery LOI</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiSio2" name="PileChemLoiSio2" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiCao" name="PileChemLoiCao" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiPhos" name="PileChemLoiPhos" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiAl2O3" name="PileChemLoiAl2O3" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiMgo" name="PileChemLoiMgo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiC" name="PileChemLoiC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiOil" name="PileChemLoiOil" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiFeo" name="PileChemLoiFeo" autocomplete="off">
                </div>
            </div>
        </form>
    </div>
    <hr class="section-divider">
</body>
</html>
[HttpPost]
        public ActionResult SaveRawMaterial(RawMaterialQuantity model)
        {           

            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                {
                    cmd.CommandType = CommandType.StoredProcedure;
                    
                    cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = model.PileNo ?? "";
                    cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = model.Source ?? "";                    
                    cmd.Parameters.Add("P_StartDate", OracleDbType.Date).Value = model.StartDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_EndDate", OracleDbType.Date).Value = model.EndDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_ConsStartDate", OracleDbType.Date).Value = model.ConsStartDate ?? (object)DBNull.Value;                    
                    cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
                    cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = model.KBFines ?? 0;
                    cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = model.NoaFines ?? 0;
                    cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = model.YardFines ?? 0;

                    cmd.ExecuteNonQuery();
                }
                conn.Close();
            }

            ViewBag.Message = "Data Saved Successfully";
            return View("RawMaterialQuantity",model); 
        }
        
