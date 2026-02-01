<!-- ================= MODAL ================= -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header">
                <h5 class="modal-title w-100 text-center">MG CLAY WEIGHTAGE</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">

                <!-- Clay 1 -->
                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY1" class="form-select">
                            <option value="">Clay1</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P1" class="form-select">
                            <option value="">%</option>
                            <option>50</option>
                            <option>100</option>
                        </select>
                    </div>
                </div>

                <!-- Clay 2 -->
                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY2" class="form-select">
                            <option value="">Clay2</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P2" class="form-select">
                            <option value="">%</option>
                            <option>50</option>
                        </select>
                    </div>
                </div>

                <!-- Clay 3 -->
                <div class="row mb-2">
                    <div class="col-6">
                        <select id="MG_CLAY3" class="form-select">
                            <option value="">Clay3</option>
                            <option>ACE</option>
                            <option>BRL</option>
                        </select>
                    </div>
                    <div class="col-6">
                        <select id="P3" class="form-select">
                            <option value="">%</option>
                        </select>
                    </div>
                </div>

            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" onclick="checkClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>
