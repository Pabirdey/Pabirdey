<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <div class="mb-3 text-center fw-bold">Weightage of Clay</div>

                <div class="row mb-3">
                    <div class="col-3">Clay1</div>
                    <div class="col-9">
                        <select id="clay1" class="form-select">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>

                <div class="row mb-3">
                    <div class="col-3">Clay2</div>
                    <div class="col-9">
                        <select id="clay2" class="form-select">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>

                <div class="row">
                    <div class="col-3">Clay3</div>
                    <div class="col-9">
                        <select id="clay3" class="form-select">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>
            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" onclick="saveClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>
