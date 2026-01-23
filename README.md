<!-- ================= MODAL ================= -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header">
                <h5 class="modal-title">Other MG Clay Type</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <label class="form-label">Enter MG Clay Type</label>
                <input type="text"
                       id="txtOtherMGClay"
                       class="form-control form-control-lg"
                       placeholder="Enter value">
                <input type="hidden" id="hdnRowIndex">
            </div>

            <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
            </div>

        </div>
    </div>
</div>
