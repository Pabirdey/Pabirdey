<div class="container-fluid mt-0">
    <div class="form-group">
        <label for="tbFDatePick" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
        <input id="tbFDatePick" size="14" style="height:28px;text-align:center">
        &nbsp;&nbsp;&nbsp;&nbsp;
        <label style="font-family:Allan,cursive;font-size:25px;">Furnace</label>
        <select id="lstFur">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <!-- Mudgun Details -->
    <div class="form-section">
        <div class="section-title">Mudgun Details</div>
        <div class="table-responsive scrollable-table" style="max-height:318px;">
            <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                <thead>
                    <tr>
                        <th class="Long_Heading_Medium">Cast No</th>
                        <th>Closure Mode</th>
                        <th>Clay Qty. Pushed</th>
                        <th>MG Clay Type</th>
                        <th>Lot No</th>
                        <th>No. of Bags</th>
                        <th>Mudgun Holding Time</th>
                        <th>Mudgun Nozzle</th>
                        <th>M.Nozzle Temp Before Closing</th>
                        <th>M.Nozzle Temp after Closing</th>
                        <th>Initial Plugin Pressure</th>
                        <th>Max Plugin Pressure</th>
                        <th>Final Plugin Pressure</th>
                        <th>Pressure On Force</th>
                        <th>Clay Leakage</th>
                        <th>Back Fire</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<!-- Modal for Other MG Clay -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Other MG Clay Type</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <input type="hidden" id="hdnRowIndex" />
                <input type="text" id="txtOtherMGClay" class="form-control form-control-lg" placeholder="Enter MG Clay Type">
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
            </div>
        </div>
    </div>
</div>
