@model YourNamespace.Models.RmbbPile
@{
    ViewBag.Title = "Raw Material Quantity";
}

<h4 class="mb-4" id="Main_Heading">Raw Material Quantity</h4>
<hr class="section-divider" />

@if (!string.IsNullOrEmpty(ViewBag.Message))
{
    <div class="alert alert-info">@ViewBag.Message</div>
}

@using (Html.BeginForm("RmbbPile", "YourControllerName", FormMethod.Post, new { id = "rawMaterialForm" }))
{
 <div class="form-group">
        <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary" />
    </div>

    @if (!string.IsNullOrEmpty(ViewBag.Message as string))
    {
        <div class="alert alert-info mt-2">
            @ViewBag.Message
        </div>
    }
}
  <div class="form-group row">
        <label class="col-sm-2 col-form-label">Source</label>
        <div class="col-sm-4">
            <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                <option value="">-- Select Source --</option>
                <option value="RMBB_KNR" @(Model?.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                <option value="RMBB" @(Model?.Source == "RMBB" ? "selected" : "")>RMBB</option>
                <option value="RMBBN" @(Model?.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
            </select>
        </div>
    </div>

 <form method="post" action="/RmbbPile/RmbbPile" id="rawMaterialForm">
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
                            <option value="RMBB_KNR" @(Model != null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>


                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="mar
    gin-left:40px;">Start Date</label>
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
                    <input class="form-control" type="text" value="@Model.NOA_FINES" name="NOA_FINES" id="NOA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JODA_FINES" name="JODA_FINES" id="JODA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KB_FINES" name="KB_FINES" id="KB_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YARD_FINES" name="YARD_FINES" id="YARD_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.TXT_BHJ" name="TXT_BHJ" id="TXT_BHJ" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.IO_NAMISA" name="IO_NAMISA" id="IO_NAMISA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text" value="@Model.IO_FORTESCUE_BF" name="IO_FORTESCUE_BF" id="IO_FORTESCUE_BF" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_NOA_CRUSHED" name="IRON_ORE_NOA_CRUSHED" id="IRON_ORE_NOA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_JODA_CRUSHED" name="IRON_ORE_JODA_CRUSHED" id="IRON_ORE_JODA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_KB_CRUSHED" name="IRON_ORE_KB_CRUSHED" id="IRON_ORE_KB_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pilbhara</label>
                    <input class="form-control" type="text" name="IO_PILBHARA" id="IO_PILBHARA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kumba</label>
                    <input class="form-control" type="text" value="@Model.IO_KUMBA" name="IO_KUMBA" id="IO_KUMBA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Third row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Coastal Fines</label>
                    <input class="form-control" type="text" value="@Model.IO_COASTAL_FINES" name="IO_COASTAL_FINES" id="IO_COASTAL_FINES" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Deobhar/ Katamati Fines</label>
                    <input class="form-control" type="text" value="@Model.KATAMATI_FINES" name="KATAMATI_FINES" id="KATAMATI_FINES" style="margin:4px;" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual S/O(Lump)</label>
                    <input class="form-control" type="text" value="@Model.IO_KIRANDUL_SIZE_ORE" name="IO_KIRANDUL_SIZE_ORE" id="IO_KIRANDUL_SIZE_ORE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kirandual Fines</label>
                    <input class="form-control" type="text" value="@Model.IO_KIRANDUL_FINES" name="IO_KIRANDUL_FINES" id="IO_KIRANDUL_FINES" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">FSF Venezuelan</label>
                    <input class="form-control" type="text" value="@Model.IO_FSF_VENEZUELAN" name="IO_FSF_VENEZUELAN" id="IO_FSF_VENEZUELAN" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">SN Feed Value</label>
                    <input class="form-control" type="text" value="@Model.IO_SN_FEED_VALE" name="IO_SN_FEED_VALE" id="IO_SN_FEED_VALE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>

            </div>
            <!-- Fourth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Other Imp Ore</label>
                    <input class="form-control" type="text" value="@Model.IO_OTHER_IMP_ORE" name="IO_OTHER_IMP_ORE" id="IO_OTHER_IMP_ORE" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Imp Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.TXT_IMP_ORE_FINES" name="TXT_IMP_ORE_FINES" id="TXT_IMP_ORE_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bacheli</label>
                    <input class="form-control" type="text" value="@Model.DO_BACHELI" name="DO_BACHELI" id="DO_BACHELI" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Jaroli</label>
                    <input class="form-control" type="text" value="@Model.DO_JAROLI_FINES" name="DO_JAROLI_FINES" id="DO_JAROLI_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kay Pee Entp</label>
                    <input class="form-control" type="text" value="@Model.DO_KAY_PEE_ENTERPRISE" name="DO_KAY_PEE_ENTERPRISE" id="DO_KAY_PEE_ENTERPRISE" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Ahluwalia Fines</label>
                    <input class="form-control" type="text" value="@Model.DO_AHLUWALIA_FINES" name="DO_AHLUWALIA_FINES" id="DO_AHLUWALIA_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Fifth row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Diatari</label>
                    <input class="form-control" type="text" value="@Model.DO_DIATARI_FINES" name="DO_DIATARI_FINES" id="DO_DIATARI_FINES" onblur="DomesticOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Domestic IOF</label>
                    <input class="form-control" type="text" value="@Model.TXT_DOMESTIC_ORE_FINES" name="TXT_DOMESTIC_ORE_FINES" id="TXT_DOMESTIC_ORE_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Iron Ore Fines</label>
                    <input class="form-control" type="text" readonly value="@Model.IO_FINES" name="IO_FINES" id="IO_FINES" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone HI Silica</label>
                    <input class="form-control" type="text" value="@Model.LS_HI_SILICA" name="LS_HI_SILICA" id="LS_HI_SILICA" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone RPD</label>
                    <input class="form-control" type="text" value="@Model.LS_RPD" name="LS_RPD" id="LS_RPD" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone SP Grade</label>
                    <input class="form-control" type="text" value="@Model.LS_SP_GRADE" name="LS_SP_GRADE" id="LS_SP_GRADE" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag(O/S)</label>
                    <input class="form-control" type="text" value="@Model.LD_SLAG_OS" name="LD_SLAG_OS" id="LD_SLAG_OS" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soap Stone</label>
                    <input class="form-control" type="text" value="@Model.SOAP_STONE" name="SOAP_STONE" id="SOAP_STONE" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone Gotan</label>
                    <input class="form-control" type="text" value="@Model.LS_GOTTAN" name="LS_GOTTAN" id="LS_GOTTAN" onblur="MixedFluxSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Limestone Stone(Imported)</label>
                    <input class="form-control" type="text" value="@Model.LIME_STONE_IMP" name="LIME_STONE_IMP" id="LIME_STONE_IMP" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestaone Himachal</label>
                    <input class="form-control" type="text" value="@Model.LS_HIMACHAL" name="LS_HIMACHAL" id="LS_HIMACHAL" style="margin:4px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Bhutan Dolo</label>
                    <input class="form-control" type="text" value="@Model.BHUTAN_DOLO" name="BHUTAN_DOLO" id="BHUTAN_DOLO" style="margin:8px;" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Gomardih Dolo</label>
                    <input class="form-control" type="text" value="@Model.GOMARDIH_DOLO" name="GOMARDIH_DOLO" id="GOMARDIH_DOLO" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone (Phillipines)</label>
                    <input class="form-control" type="text" value="@Model.LS_PHILLIPINES" name="LS_PHILLIPINES" id="LS_PHILLIPINES" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite(Local)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_LOCAL" name="PYROXENITE_LOCAL" id="PYROXENITE_LOCAL" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite (Sukinda)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_SUKINDA" name="PYROXENITE_SUKINDA" id="PYROXENITE_SUKINDA" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pyroxenite  (Imp)</label>
                    <input class="form-control" type="text" value="@Model.PYROXENITE_IMPORTED" name="PYROXENITE_IMPORTED" id="PYROXENITE_IMPORTED" onblur="MixedFluxSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Limestone(CP Gr.)</label>
                    <input class="form-control" type="text" value="@Model.LS_CP_GRADE" name="LS_CP_GRADE" id="LS_CP_GRADE" onblur="MixedFluxSum()" style="margin:8px;" autocomplete="off">
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
                    <input class="form-control" type="text" readonly value="@Model.MIXED_FLUX" name="MIXED_FLUX" id="MIXED_FLUX" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">LD Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.LD_SLUDGE" name="LD_SLUDGE" id="LD_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Scale</label>
                    <input class="form-control" type="text" readonly value="@Model.MILL_SCALE" name="MILL_SCALE" id="MILL_SCALE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Kiln Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.KILN_DUST" name="KILN_DUST" id="KILN_DUST" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Solid Waste</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" value="@Model.SOLID_WASTE" name="SOLID_WASTE" id="SOLID_WASTE" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                @*<div class="col-md-2" id="pswBlock1" style="display:none">
                        <label class="form-label">PSW1</label>
                        <input class="form-control" type="text" value="@Model.PSW1" name="PSW1" id="PSW1" onblur="SolidWasteSum()" autocomplete="off">
                    </div>*@
                <div class="col-md-2" id="pswBlock1">
                    <label class="form-label">PSW1</label>
                    <input class="form-control" type="text" value="@Model.PSW1" name="PSW1" id="PSW1" onblur="SolidWasteSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mill Sludge</label>
                    <input class="form-control" type="text" readonly value="@Model.MILL_SLUDGE" name="MILL_SLUDGE" id="MILL_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Flue Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.FLUE_DUST" name="FLUE_DUST" id="FLUE_DUST" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Esp Dust</label>
                    <input class="form-control" type="text" readonly value="@Model.ESP_DUST" name="ESP_DUST" id="ESP_DUST" autocomplete="off">
                </div>
                <div class="col-md-1">
                </div>
                <div class="col-md-2">
                </div>
                <div class="col-md-1">
                    <button type="button" class="btn btn-warning">OK</button>
                </div>
                @*<div class="col-md-2" id="pswBlock2" style="display:none">
                        <label class="form-label">PSW_CONS2</label>
                        <input class="form-control" type="text" value="@Model.PSW_CONS2" name="PSW_CONS2" id="PSW_CONS2" onblur="SolidWasteSum()" autocomplete="off">
                    </div>*@
                <div class="col-md-2" id="pswBlock2">
                    <label class="form-label">PSW_CONS2</label>
                    <input class="form-control" type="text" value="@Model.PSW_CONS2" name="PSW_CONS2" id="PSW_CONS2" onblur="SolidWasteSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">GCP Sludge</label>
                    <input class="form-control" type="text" value="@Model.GCP_SLUDGE" name="GCP_SLUDGE" id="GCP_SLUDGE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Fresh</label>
                    <input class="form-control" type="text" value="@Model.LD_SLUDGE_FRESH" name="LD_SLUDGE_FRESH" id="LD_SLUDGE_FRESH" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Lime Fines</label>
                    <input class="form-control" type="text" value="@Model.LIME_FINES" name="LIME_FINES" id="LIME_FINES" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Slag Fines</label>
                    <input class="form-control" type="text" value="@Model.LD_SLAG_FINES" name="LD_SLAG_FINES" id="LD_SLAG_FINES" autocomplete="off">
                </div>
                <div class="col-md-2">
                </div>
                <div class="col-md-2" id="pswBlock3">
                    <label class="form-label">Blend-I</label>
                    @*<select id="LstBlend1" value="@Model.PSW_BL1" name="PSW_BL1">
                        </select>*@
                    <select id="PSW_BL1" class="form-control">
                        <option value="@Model.PSW_BL1" name="PSW_BL1">Blend-I</option>
                        <option value="1">1</option>
                        <option value="2">2</option>
                        <option value="3">3</option>
                        <option value="4">4</option>
                        <option value="5">5</option>
                        <option value="6">6</option>
                        <option value="7">7</option>
                        <option value="8">8</option>
                        <option value="9">9</option>
                        <option value="10">10</option>
                        <option value="11">11</option>
                        <option value="12">12</option>
                        <option value="13">13</option>
                        <option value="14">14</option>
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
                    <input class="form-control" type="text" value="@Model.DOLO_FINES" name="DOLO_FINES" id="DOLO_FINES" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Flue Dust</label>
                    <input class="form-control" type="text" value="@Model.FLUE_DUST_PRM" name="FLUE_DUST_PRM" id="FLUE_DUST_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Sludge</label>
                    <input class="form-control" type="text" value="@Model.MILL_SLUDGE_PRM" name="MILL_SLUDGE_PRM" id="MILL_SLUDGE_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">ESP Dust</label>
                    <input class="form-control" type="text" value="@Model.ESP_DUST_PRM" name="ESP_DUST_PRM" id="ESP_DUST_PRM" oninput="CopyValue()" autocomplete="off">
                </div>
                <div class="col-md-2" id="pswBlock4">
                    <label class="form-label">Blend-II</label>
                    <select id="PSW_BL2" class="form-control">
                        <option value="">Blend-II</option>
                        <option value="1">1</option>
                        <option value="2">2</option>
                        <option value="3">3</option>
                        <option value="4">4</option>
                        <option value="5">5</option>
                        <option value="6">6</option>
                        <option value="7">7</option>
                        <option value="8">8</option>
                        <option value="9">9</option>
                        <option value="10">10</option>
                        <option value="11">11</option>
                        <option value="12">12</option>
                        <option value="13">13</option>
                        <option value="14">14</option>
                    </select>
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Revert Material</label>
                    <input class="form-control" type="text" readonly value="@Model.REVERT_MAT" name="REVERT_MAT" id="REVERT_MAT" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">LD Sludge Mix</label>
                    <input class="form-control" type="text" value="@Model.LD_SLUDGE_MIX_PRM" name="LD_SLUDGE_MIX_PRM" id="LD_SLUDGE_MIX_PRM" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Soild Mix</label>
                    <input class="form-control" type="text" value="@Model.SOLID_MIX" name="SOLID_MIX" id="SOLID_MIX" oninput="REVERT_MATSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Mill Scale</label>
                    <input class="form-control" type="text" value="@Model.MILL_SCALE_PRM" name="MILL_SCALE_PRM" id="MILL_SCALE_PRM" autocomplete="off">
                    <input class="form-control" type="text" value="" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Kiln Dust</label>
                    <input class="form-control" type="text" value="@Model.KILN_DUST_PRM" name="KILN_DUST_PRM" id="KILN_DUST_PRM" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Coke Breeze</label>
                    <input class="form-control" type="text" readonly value="@Model.COKE_BREEZE" name="COKE_BREEZE" id="COKE_BREEZE" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">RPC</label>
                    <input class="form-control" type="text" readonly value="@Model.RPC" name="RPC" id="RPC" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Jhama Coal</label>
                    <input class="form-control" type="text" readonly value="@Model.JHAMA" name="JHAMA" id="JHAMA" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">G Sinter Fines</label>
                    <input class="form-control" type="text" value="@Model.G_SINTER_FINES" name="G_SINTER_FINES" id="G_SINTER_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Pellet SN Fines</label>
                    <input class="form-control" type="text" value="@Model.G_PELLET_FINES" name="G_PELLET_FINES" id="G_PELLET_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">G ORE Fines</label>
                    <input class="form-control" type="text" value="@Model.G_ORE_FINES" name="G_ORE_FINES" id="G_ORE_FINES" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM(End Cone)</label>
                    <input class="form-control" type="text" value="@Model.BM_END_CONE" name="BM_END_CONE" id="BM_END_CONE" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Anthracite</label>
                    <input class="form-control" type="text" value="@Model.ANTHRACITE" name="ANTHRACITE" id="ANTHRACITE" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BM Previous</label>
                    <input class="form-control" type="text" value="@Model.BM_PREVIOUS" name="BM_PREVIOUS" id="BM_PREVIOUS" onblur="MIXED_MATERIALSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Mixed Material</label>
                    <input class="form-control" type="text" readonly value="@Model.MIXED_MATERIAL" name="MIXED_MATERIAL" id="MIXED_MATERIAL" oninput="TOTAL_PILEsum()" autocomplete="off">
                </div>
            </div>
            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.BM_SIO2_PLANT" name="BM_SIO2_PLANT" id="BM_SIO2_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.BM_CAO_PLANT" name="BM_CAO_PLANT" id="BM_CAO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.BM_PHOS_PLANT" name="BM_PHOS_PLANT" id="BM_PHOS_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.BM_AL2O3_PLANT" name="BM_AL2O3_PLANT" id="BM_AL2O3_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label" style="color:#ff6a00">Total Pile</label>
                    <input class="form-control" type="text" style="background-color:#ffd800;border:1px solid black;" readonly value="@Model.TOTAL_PILE" name="TOTAL_PILE" id="TOTAL_PILE" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">No Of Layers</label>
                    <input class="form-control" type="text" value="@Model.NoOfLayer" name="NoOfLayer" id="NoOfLayer" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.BM_MGO_PLANT" name="BM_MGO_PLANT" id="BM_MGO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.BM_C_PLANT" name="BM_C_PLANT" id="BM_C_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.BM_OIL_PLANT" name="BM_OIL_PLANT" id="BM_OIL_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.BM_FEO_PLANT" name="BM_FEO_PLANT" id="BM_FEO_PLANT" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary" />
                </div>
            </div>

            <hr class="section-divider">
            <div class="row material-row mb-2">
                <h6>Pile Chemistery LOI</h6>
                <div class="col-md-2">
                    <label class="form-label">Sio2</label>
                    <input class="form-control" type="text" value="@Model.BM_SIO2_PLANT_LOI" name="BM_SIO2_PLANT_LOI" id="BM_SIO2_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Cao</label>
                    <input class="form-control" type="text" value="@Model.BM_CAO_PLANT_LOI" name="BM_CAO_PLANT_LOI" id="BM_CAO_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Phos</label>
                    <input class="form-control" type="text" value="@Model.BM_PHOS_PLANT_LOI" name="BM_PHOS_PLANT_LOI" id="BM_PHOS_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Al2o3</label>
                    <input class="form-control" type="text" value="@Model.BM_AL2O3_PLANT_LOI" name="BM_AL2O3_PLANT_LOI" id="BM_AL2O3_PLANT_LOI" autocomplete="off">
                </div>
            </div>
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.BM_MGO_PLANT_LOI" name="BM_MGO_PLANT_LOI" id="BM_MGO_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.BM_C_PLANT_LOI" name="BM_C_PLANT_LOI" id="BM_C_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.BM_OIL_PLANT_LOI" name="BM_OIL_PLANT_LOI" id="BM_OIL_PLANT_LOI" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.BM_FEO_PLANT_LOI" name="BM_FEO_PLANT_LOI" id="BM_FEO_PLANT_LOI" autocomplete="off">
                </div>
            </div>
        </form>
