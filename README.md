<div class="modal fade" id="BinDetailsmodal" tabindex="-1" data-bs-backdrop="static" data-bs-keyboard="false">
        <div class="modal-dialog modal-xl custom-modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h3 class="modal-title w-100 text-center" style="font-family:Allan,cursive;">Bin Details Master</h3>                                        
                </div>      
                <div class="modal-Furnace">
                    <h3 class="modal-title w-20" style="font-family:Courier New, Courier, monospace;margin-left:20px;font-weight:bold;">Furnace:-</h3>                                                                                   
                        <select id="ddlFurnace">
                            <option value="C">C</option>
                            <option value="E">E</option>
                            <option value="F">F</option>
                        </select>                    
                </div>          
                <div class="modal-body">
                    <table id="tblBinDetails" class="table table-bordered" style="font-family:Courier New; font-weight:bold;">                        
                        <thead>
                            <tr>
                                <th style="width:40px;">FUR NAME</th>
                                <th style="width:40px;">iMONITOR TAG ID</th>
                                <th style="width:70px;">iHISTORIAN TAG NAME</th>
                                <th style="width:40px;">WEB COLUMN</th>
                                <th style="width:40px;">TAG TYPE</th>
                                <th style="width:40px;">REQUIRED</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn-Modalsave" onclick="btnSaveBinRequired()">Save</button>
                    <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>
