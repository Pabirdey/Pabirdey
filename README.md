@model ProcessTrends.Models.RawMaterialQuantity
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Quantity</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">    
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
        .form-control{            
            border-radius:6px;
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
                        <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
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
                        <input type="text" class="form-control" name="StartDate" id="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="text" class="form-control" name="EndDate" id="EndDate" value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="text" class="form-control" name="ConsStartDate" id="ConsStartDate" value="@(Model.ConsStartDate.HasValue ? Model.ConsStartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NoaFines" name="NoaFines" id="NoaFines" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JodaFines" name="JodaFines" id="JodaFines" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KBFines" name="KBFines" id="KBFines" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YardFines" name="YardFines" id="YardFines" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.BHJ" name="BHJ" id="BHJ" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.Namisa" name="Namisa" id="Namisa" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text" value="@Model.FortescueBF" name="FortescueBF" id="FortescueBF" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text" value="@Model.NoaCrushed" name="NoaCrushed" id="NoaCrushed" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text" value="@Model.JodaCrushed" name="JodaCrushed" id="JodaCrushed" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text" value="@Model.KbCrushed" name="KbCrushed" id="KbCrushed" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text" name="Pilbhara" id="Pilbhara" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text" value="@Model.Kumba" name="Kumba" id="Kumba" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Third row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coastal Fines</label>
                    <input class="form-control" type="text" value="@Model.CoastalFines" name="CoastalFines" id="CoastalFines" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Deobhar/ Katamati Fines</label>
                    <input class="form-control" type="text" value="@Model.KatamatiFines" name="KatamatiFines" id="KatamatiFines" style="margin:4px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual S/O(Lump)</label>
                    <input class="form-control" type="text" value="@Model.KirandulLump" name="KirandulLump" id="KirandulLump" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual Fines</label>
                    <input class="form-control" type="text" value="@Model.KirandulFines" name="KirandulFines" id="KirandulFines" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">FSF Venezuelan</label>
                    <input class="form-control" type="text" value="@Model.FSFVenezuelan" name="FSFVenezuelan" id="FSFVenezuelan" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">SN Feed Value</label>
                    <input class="form-control" type="text" value="@Model.SnFeedValue" name="SnFeedValue" id="SnFeedValue" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>

            </div>
            <!-- Fourth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Other Imp Ore</label>
                    <input class="form-control" type="text" value="@Model.OtherImpOre" name="OtherImpOre" id="OtherImpOre" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Imp Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.ImpOreFines" name="ImpOreFines" id="ImpOreFines" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bacheli</label>
                    <input class="form-control" type="text" value="@Model.Bacheli" name="Bacheli" id="Bacheli" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jaroli</label>
                    <input class="form-control" type="text" value="@Model.Jaroli" name="Jaroli" id="Jaroli" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kay Pee Entp</label>
                    <input class="form-control" type="text" value="@Model.KayPeeEntp" name="KayPeeEntp" id="KayPeeEntp" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Ahluwalia Fines</label>
                    <input class="form-control" type="text" value="@Model.AhluwaliaFines" name="AhluwaliaFines" id="AhluwaliaFines" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>                
            </div>
            <!-- Fifth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Diatari</label>
                    <input class="form-control" type="text" value="@Model.Daitari" name="Daitari" id="Daitari" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Domestic IOF</label>
                    <input class="form-control" type="text" value="@Model.DomesticIOF" name="DomesticIOF" id="DomesticIOF" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Iron Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.IronOreFines" name="IronOreFines" id="IronOreFines" oninput="TotalPilesum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone HI Silica</label>
                    <input class="form-control" type="text" value="@Model.LimestoneHISilica" name="LimestoneHISilica" id="LimestoneHISilica" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone RPD</label>
                    <input class="form-control" type="text" value="@Model.LimestoneRPD" name="LimestoneRPD" id="LimestoneRPD" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone SP Grade</label>
                    <input class="form-control" type="text" value="@Model.LimestoneSPGrade" name="LimestoneSPGrade" id="LimestoneSPGrade" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag(O/S)</label>
                    <input class="form-control" type="text" value="@Model.LDSlagOs" name="LDSlagOs" id="LDSlagOs" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soap Stone</label>
                    <input class="form-control" type="text" value="@Model.SoapStone" name="SoapStone" id="SoapStone" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone Gotan</label>
                    <input class="form-control" type="text" value="@Model.LimestoneGotan" name="LimestoneGotan" id="LimestoneGotan" onblur="MixedFluxSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone Stone(Imported)</label>
                    <input class="form-control" type="text" value="@Model.LimestoneImp" name="LimestoneImp" id="LimestoneImp" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone Himachal</label>
                    <input class="form-control" type="text" value="@Model.LimestoneHimachal" name="LimestoneHimachal" id="LimestoneHimachal" style="margin:4px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bhutan Dolo</label>
                    <input class="form-control" type="text" value="@Model.BhutanDolo" name="BhutanDolo" id="BhutanDolo" style="margin:8px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Gomardih Dolo</label>
                    <input class="form-control" type="text" value="@Model.GomardihDolo" name="GomardihDolo" id="GomardihDolo" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone (Phillipines)</label>
                    <input class="form-control" type="text" value="@Model.LimestonePhilipines" name="LimestonePhilipines" id="LimestonePhilipines" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite(Local)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteLocal" name="PyroxeniteLocal" id="PyroxeniteLocal" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite (Sukinda)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteSukinda" name="PyroxeniteSukinda" id="PyroxeniteSukinda" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite  (Imp)</label>
                    <input class="form-control" type="text" value="@Model.PyroxeniteImp" name="PyroxeniteImp" id="PyroxeniteImp" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone(CP Gr.)</label>
                    <input class="form-control" type="text" value="@Model.LimestoneCPGr" name="LimestoneCPGr" id="LimestoneCPGr" onblur="MixedFluxSum()" style="margin:8px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Olivine</label>
                    <input class="form-control" type="text" value="@Model.Olivine" name="Olivine" id="Olivine" onblur="MixedFluxSum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Flux</label>
                    <input class="form-control" type="text" readonly value="@Model.MixedFlux" name="MixedFlux" id="MixedFlux" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">LD Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.LdSludge" name="LdSludge" id="LdSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Scale</label>
                    <input class="form-control" type="text" readonly value="@Model.MillScale1" name="MillScale1" id="MillScale1" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Kiln Dust</label> 
                    <input class="form-control" type="text" readonly value="@Model.Kilndust" name="Kilndust" id="Kilndust" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Solid Waste</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" value="@Model.SolidWaste" name="SolidWaste" id="SolidWaste" oninput="RevertMatSum()"  autocomplete="off">
                </div>                
                    <div class="col-md-2" id="pswBlock1" style="display:none">
                        <label class="form-label">PSW1</label>
                        <input class="form-control" type="text" value="@Model.PSW1" name="PSW1" id="PSW1" onblur="SolidWasteSum()" autocomplete="off">
                    </div>                
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.MillSludge" name="MillSludge" id="MillSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Flue Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.Fluedust" name="Fluedust" id="Fluedust" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Esp Dust</label> 
                    <input class="form-control" type="text" readonly value="@Model.ESPdust" name="ESPdust" id="ESPdust" autocomplete="off">
                </div>
                <div class="col-md-1">
                </div>
                <div class="col-md-2">
                </div>
                <div class="col-md-1">
                    <button type="button" class="btn btn-warning">OK</button>
                </div>
                <div class="col-md-2" id="pswBlock2" style="display:none">
                    <label class="form-label">PSW2</label>
                    <input class="form-control" type="text" value="@Model.PSW2" name="PSW2" id="PSW2" onblur="SolidWasteSum()" autocomplete="off">
                </div>   
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">GCP Sludge</label>
                    <input class="form-control" type="text" value="@Model.GCPSludge" name="GCPSludge" id="GCPSludge" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Fresh</label>
                    <input class="form-control" type="text" value="@Model.LDSludgeFresh" name="LDSludgeFresh" id="LDSludgeFresh" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Lime Fines</label>
                    <input class="form-control" type="text" value="@Model.LimeFines" name="LimeFines" id="LimeFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag Fines</label>
                    <input class="form-control" type="text" value="@Model.LDSlagFines" name="LDSlagFines" id="LDSlagFines" autocomplete="off">
                </div>
                <div class="col-md-2">                   
                </div>
                <div class="col-md-2" id="pswBlock3" style="display:none">
                    <label class="form-label">Blend-I</label>
                    @*<select id="LstBlend1" value="@Model.PSW_BL1" name="PSW_BL1">
                    </select>*@
                    <select id="blend1" class="form-control">
                        <option value="@Model.PSW_BL1" name="PSW_BL1">Select Blend-I</option> 
                    </select>
                </div>   
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">WRP</label>
                    <input class="form-control" type="text" value="@Model.WRP" name="WRP" id="WRP" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Dolo Fines</label>
                    <input class="form-control" type="text" value="@Model.DoloFines" name="DoloFines" id="DoloFines" oninput="RevertMatSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Flue Dust</label>
                    <input class="form-control" type="text" value="@Model.FlueDustPrm" name="FlueDustPrm" id="FlueDustPrm" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Sludge</label>
                    <input class="form-control" type="text" value="@Model.MillSludgePrm" name="MillSludgePrm" id="MillSludgePrm"  oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">ESP Dust</label>
                    <input class="form-control" type="text" value="@Model.ESPDustPrm" name="ESPDustPrm" id="ESPDustPrm" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2" id="pswBlock4" style="display:none">
                    @*<label class="form-label">BlendII</label>
                    <select id="LstBlend2" value="@Model.PSW_BL2" name="PSW_BL2">
                      </select>*@
                    <label class="form-label">Blend-II</label>
                    @*<select id="LstBlend1" value="@Model.PSW_BL1" name="PSW_BL1">
        </select>*@
                    <select id="blend1" class="form-control">
                        <option value="">Select Blend-I</option>
                    </select>
                </div>  
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Revert Material</label>
                    <input class="form-control" type="text" readonly value="@Model.RevertMat" name="RevertMat" id="RevertMat" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Mix</label>
                    <input class="form-control" type="text" value="@Model.LDSludgeMix" name="LDSludgeMix" id="LDSludgeMix" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soild Mix</label>
                    <input class="form-control" type="text" value="@Model.SolidMix" name="SolidMix" id="SolidMix" oninput="RevertMatSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Scale</label>
                    <input class="form-control" type="text" value="@Model.MIllScale" name="MIllScale" id="MIllScale" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kiln Dust</label>
                    <input class="form-control" type="text" value="@Model.KilnDust1" name="KilnDust1" id="KilnDust1" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Coke Breeze</label>
                    <input class="form-control" type="text" readonly value="@Model.CokeBreeze" name="CokeBreeze" id="CokeBreeze" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">RPC</label>
                    <input class="form-control" type="text" readonly value="@Model.RPC" name="RPC" id="RPC" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Jhama Coal</label>
                    <input class="form-control" type="text" readonly value="@Model.JhamaCoal" name="JhamaCoal" id="JhamaCoal" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">G Sinter Fines</label>
                    <input class="form-control" type="text" value="@Model.GSinterFines" name="GSinterFines" id="GSinterFines" onblur="MixedMaterialSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pellet SN Fines</label>
                    <input class="form-control" type="text" value="@Model.PelletSNFines" name="PelletSNFines" id="PelletSNFines" onblur="MixedMaterialSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">G ORE Fines</label>
                    <input class="form-control" type="text" value="@Model.GOreFines" name="GOreFines" id="GOreFines" onblur="MixedMaterialSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM(End Cone)</label>
                    <input class="form-control" type="text" value="@Model.BMEndCone" name="BMEndCone" id="BMEndCone" onblur="MixedMaterialSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Anthracite</label>
                    <input class="form-control" type="text" value="@Model.Anthracite" name="Anthracite" id="Anthracite" oninput="TotalPilesum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM Previous</label>
                    <input class="form-control" type="text" value="@Model.BMPrevious" name="BMPrevious" id="BMPrevious" onblur="MixedMaterialSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Material</label>
                    <input class="form-control" type="text" readonly value="@Model.MixedMaterial" name="MixedMaterial" id="MixedMaterial" oninput="TotalPilesum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.PileChemSio2" name="PileChemSio2" id="PileChemSio2" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.PileChemCao" name="PileChemCao" id="PileChemCao" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.PileChemPhos" name="PileChemPhos" id="PileChemPhos" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.PileChemAl2O3" name="PileChemAl2O3" id="PileChemAl2O3" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Total Pile</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" readonly value="@Model.TotalPile" name="TotalPile" id="TotalPile" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">No Of Layers</label> 
                    <input class="form-control" type="text" value="@Model.NoOfLayer" name="NoOfLayer" id="NoOfLayer" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">               
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.PileChemMgo" name="PileChemMgo" id="PileChemMgo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.PileChemC" name="PileChemC" id="PileChemC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.PileChemOil" name="PileChemOil" id="PileChemOil" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.PileChemFeo" name="PileChemFeo" id="PileChemFeo" autocomplete="off">
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
                    <input class="form-control" type="text" value="@Model.PileChemLoiSio2" name="PileChemLoiSio2" id="PileChemLoiSio2" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiCao" name="PileChemLoiCao" id="PileChemLoiCao" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiPhos" name="PileChemLoiPhos" id="PileChemLoiPhos" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiAl2O3" name="PileChemLoiAl2O3" id="PileChemLoiAl2O3" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiMgo" name="PileChemLoiMgo" id="PileChemLoiMgo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiC" name="PileChemLoiC" id="PileChemLoiC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiOil" name="PileChemLoiOil" id="PileChemLoiOil" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.PileChemLoiFeo" name="PileChemLoiFeo" id="PileChemLoiFeo" autocomplete="off">
                </div>
            </div>
        </form>
    </div>
    <hr class="section-divider">
    <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
</body>
</html>
<script>
    flatpickr("#StartDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true
    });

    flatpickr("#EndDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true
    });

    flatpickr("#ConsStartDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i",
        time_24hr: true
    });

    //DisplayPswBlock();

    
    function DomesticOreFinesSum() {
        var n1 = parseFloat(document.getElementById("Bacheli").value) || 0;
        var n2 = parseFloat(document.getElementById("Jaroli").value) || 0;
        var n3 = parseFloat(document.getElementById("Daitari").value) || 0;
        var n4 = parseFloat(document.getElementById("KayPeeEntp").value) || 0;
        var n5 = parseFloat(document.getElementById("AhluwaliaFines").value) || 0;
        var tot_DomesticIOF = n1 + n2 + n3 + n4 + n5;
        document.getElementById("DomesticIOF").value = tot_DomesticIOF;

    }

    function IMPOreFinesSum() {
        var n1 = parseFloat(document.getElementById("Namisa").value) || 0;
        var n2 = parseFloat(document.getElementById("CoastalFines").value) || 0;
        var n3 = parseFloat(document.getElementById("FortescueBF").value) || 0;
        var n4 = parseFloat(document.getElementById("Pilbhara").value) || 0;
        var n5 = parseFloat(document.getElementById("SnFeedValue").value) || 0;
        var n6 = parseFloat(document.getElementById("FSFVenezuelan").value) || 0;
        var n7 = parseFloat(document.getElementById("Kumba").value) || 0;
        var n8 = parseFloat(document.getElementById("KirandulFines").value) || 0;
        var n9 = parseFloat(document.getElementById("KirandulLump").value) || 0;
        var n10 = parseFloat(document.getElementById("OtherImpOre").value) || 0;
        var tot_IMPOreFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10;
        document.getElementById("ImpOreFines").value = tot_IMPOreFines;
    }
    
    function IOFinesSum() {
        var n1 = parseFloat(document.getElementById("NoaFines").value) || 0;
        var n2 = parseFloat(document.getElementById("JodaFines").value) || 0;
        var n3 = parseFloat(document.getElementById("KBFines").value) || 0;
        var n4 = parseFloat(document.getElementById("YardFines").value) || 0;
        var n5 = parseFloat(document.getElementById("BHJ").value) || 0;
        var n6 = parseFloat(document.getElementById("NoaCrushed").value) || 0;
        var n7 = parseFloat(document.getElementById("JodaCrushed").value) || 0;
        var n8 = parseFloat(document.getElementById("KbCrushed").value) || 0;
        var n9 = parseFloat(document.getElementById("ImpOreFines").value) || 0;
        var n10 = parseFloat(document.getElementById("DomesticIOF").value) || 0;
        var n11 = parseFloat(document.getElementById("KatamatiFines").value) || 0;
        var tot_IOFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11;
        document.getElementById("IronOreFines").value = tot_IOFines;
        TotalPilesum();
    }
    
    function MixedFluxSum() {
        var n1 = parseFloat(document.getElementById("LimestoneHISilica").value) || 0;
        var n2 = parseFloat(document.getElementById("LimestoneRPD").value) || 0;
        var n3 = parseFloat(document.getElementById("LimestoneSPGrade").value) || 0;
        var n4 = parseFloat(document.getElementById("LimestoneGotan").value) || 0;
        var n5 = parseFloat(document.getElementById("BhutanDolo").value) || 0;
        var n6 = parseFloat(document.getElementById("LimestoneHimachal").value) || 0;
        var n7 = parseFloat(document.getElementById("PyroxeniteLocal").value) || 0;
        var n8 = parseFloat(document.getElementById("PyroxeniteImp").value) || 0;
        var n9 = parseFloat(document.getElementById("PyroxeniteSukinda").value) || 0;
        var n10 = parseFloat(document.getElementById("SoapStone").value) || 0;
        var n11 = parseFloat(document.getElementById("LDSlagOs").value) || 0;
        var n12 = parseFloat(document.getElementById("LimestoneImp").value) || 0;
        var n13 = parseFloat(document.getElementById("LimestonePhilipines").value) || 0;
        var n14 = parseFloat(document.getElementById("LimestoneCPGr").value) || 0;
        var n15 = parseFloat(document.getElementById("GomardihDolo").value) || 0;
        var n16 = parseFloat(document.getElementById("Olivine").value) || 0;
        var tot_MixedFlux = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11 + n12 + n13 + n14 + n15 + n16;
        document.getElementById("MixedFlux").value = tot_MixedFlux;
        TotalPilesum();
    }
    
    function MixedMaterialSum() {
        var n1 = parseFloat(document.getElementById("PelletSNFines").value) || 0;
        var n2 = parseFloat(document.getElementById("GSinterFines").value) || 0;
        var n3 = parseFloat(document.getElementById("GOreFines").value) || 0;
        var n4 = parseFloat(document.getElementById("BMEndCone").value) || 0;
        var n5 = parseFloat(document.getElementById("BMPrevious").value) || 0;
        var tot_MixedMaterial = n1 + n2 + n3 + n4 + n5;
        document.getElementById("MixedMaterial").value = tot_MixedMaterial;
        TotalPilesum();
    }

    function TotalPilesum() {        
        var n1 = parseFloat(document.getElementById("IronOreFines").value) || 0;     
        var n2 = parseFloat(document.getElementById("MixedFlux").value) || 0;
        var n3 = parseFloat(document.getElementById("RevertMat").value) || 0;
        var n4 = parseFloat(document.getElementById("CokeBreeze").value) || 0;
        var n5 = parseFloat(document.getElementById("MixedMaterial").value) || 0;
        var n6 = parseFloat(document.getElementById("RPC").value) || 0;
        var n7 = parseFloat(document.getElementById("JhamaCoal").value) || 0;
        var n8 = parseFloat(document.getElementById("Anthracite").value) || 0;                
        var tot_TotalPile = n1 + n2 + n3 + n4 + n5 + n6+ n7 + n8;
        document.getElementById("TotalPile").value = tot_TotalPile;
    }
    function RevertMatSum() {
        var n1 = parseFloat(document.getElementById("DoloFines").value) || 0;
        var n2 = parseFloat(document.getElementById("SolidMix").value) || 0;
        var n3 = parseFloat(document.getElementById("SolidWaste").value) || 0;
        var tot_RevertMat = n1 + n2 + n3;
        document.getElementById("RevertMat").value = tot_RevertMat;
        TotalPilesum();
    }    
   
    function SolidWasteSum(){
        var n1 = parseFloat(document.getElementById("PSW1").value)||0;
        var n2 = parseFloat(document.getElementById("PSW2").value)||0;
        var Tot_SolidWaste = n1 + n2;
        document.getElementById("SolidWaste").value = Tot_SolidWaste;
        RevertMatSum();
    }
    function CopyValue() {
        var n1 = parseFloat(document.getElementById("LDSludgeFresh").value);
        var n2 = parseFloat(document.getElementById("FlueDustPrm").value);
        var n3 = parseFloat(document.getElementById("ESPDustPrm").value);
        var n4 = parseFloat(document.getElementById("MillSludgePrm").value);
        document.getElementById("LdSludge").value = n1;
        document.getElementById("Fluedust").value = n2;
        document.getElementById("ESPdust").value = n3;
        document.getElementById("MillSludge").value = n4;
    }
    function DisplayPswBlock() {
        debugger;
        var source = document.getElementById("SourceSelect").value;
        var block1 = document.getElementById("pswBlock1");
        var block2 = document.getElementById("pswBlock2");
        var block3 = document.getElementById("pswBlock3");
        var block4 = document.getElementById("pswBlock4");
        if (source === 'RMBB_KNR') {
            block1.style.display = "block";
            block2.style.display = "block";
            block3.style.display = "block";
            block4.style.display = "block";
        } else {
            block1.style.display = "none";
            block2.style.display = "none";
            block3.style.display = "none";
            block4.style.display = "none";
        }
    }
    



</script>
