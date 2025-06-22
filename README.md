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
