.modal-content {
    border-radius: 25px;
    border: none;
}

.modal-header {
    background: #0d6efd;
    color: #fff;
    border-radius: 25px 25px 0 0;
}

.btn-Modalsave {
    background: #198754;
    color: white;
    padding: 8px 30px;
    border-radius: 20px;
}

.btn-Modalexit {
    background: #dc3545;
    color: white;
    padding: 8px 30px;
    border-radius: 20px;
}

/* 🔥 New CSS */
.custom-modal {
    margin-top: 5px !important;
    max-width: 95% !important;
}
<div class="modal fade" id="bindetailsmodal" tabindex="-1">
    <div class="modal-dialog modal-xl custom-modal">
        <div class="modal-content">

            <div class="modal-header">
                <h5 class="modal-title w-100 text-center" style="font-family:Allan,cursive;">
                    Bin Details Master
                </h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <table id="tblBinDetails" class="table table-bordered"
                       style="font-family:Courier New; font-weight:bold;">
                    <thead>
                        <tr>
                            <th>iMONITOR TAG ID</th>
                            <th>iHISTORIAN TAG NAME</th>
                            <th>WEB COLUMN</th>
                            <th>TAG TYPE</th>
                            <th>REQUIRED</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn-Modalsave" onclick="checkClay()">Save</button>
                <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>