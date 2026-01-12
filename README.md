<!-- ================= CLAY WEIGHTAGE MODAL ================= -->
<div class="modal fade" id="clayModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content" style="border-radius:25px;">

            <!-- HEADER -->
            <div class="modal-header bg-primary text-white"
                 style="border-radius:25px 25px 0 0;">
                <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                <button type="button"
                        class="btn-close btn-close-white"
                        data-bs-dismiss="modal"></button>
            </div>

            <!-- BODY -->
            <div class="modal-body">

                <div class="text-center mb-3"
                     style="background:#0d6efd;color:white;
                            border-radius:20px;padding:8px;
                            font-weight:600;">
                    Weightage of Clay
                </div>

                <div style="background:#0d6efd;
                            border-radius:25px;
                            padding:20px;color:white;">

                    <!-- CLAY 1 -->
                    <div class="row mb-3 align-items-center">
                        <div class="col-3 fw-bold">Clay 1</div>
                        <div class="col-9">
                            <select class="form-select" id="clay1">
                                <option value="">-- Select Clay --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                    </div>

                    <!-- CLAY 2 -->
                    <div class="row mb-3 align-items-center">
                        <div class="col-3 fw-bold">Clay 2</div>
                        <div class="col-9">
                            <select class="form-select" id="clay2">
                                <option value="">-- Select Clay --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                    </div>

                    <!-- CLAY 3 -->
                    <div class="row align-items-center">
                        <div class="col-3 fw-bold">Clay 3</div>
                        <div class="col-9">
                            <select class="form-select" id="clay3">
                                <option value="">-- Select Clay --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                    </div>

                </div>
            </div>

            <!-- FOOTER -->
            <div class="modal-footer justify-content-center">
                <button type="button"
                        class="btn btn-success px-4"
                        onclick="saveData()">Save</button>

                <button type="button"
                        class="btn btn-danger px-4"
                        data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>
<!-- ======================================================= -->
