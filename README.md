<fieldset class="border rounded p-3 shadow-sm mb-4">
    <legend class="float-none w-auto px-2">
        Exception Cast
    </legend>

    <div class="d-flex justify-content-between align-items-center mb-2">
        <span></span>
        <button type="button" class="btn btn-success btn-sm" onclick="saveExceptionCast()">
            Save
        </button>
    </div>

    <div class="table-responsive scrollable-table" style="max-height:282px;">
        <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
            <thead>
                <tr>
                    <th style="width:100px;min-width:100px;box-sizing:border-box;">ID No</th>
                    <th>Taphole No</th>
                    <th style="width:150px;min-width:150px;box-sizing:border-box;">Date Time</th>
                    <th style="width:100px;min-width:100px;box-sizing:border-box;">HH24</th>
                    <th style="width:100px;min-width:100px;box-sizing:border-box;">MM</th>
                    <th>Taphole Length</th>
                    <th>Clay Paused</th>
                    <th style="width:180px;min-width:180px;box-sizing:border-box;">Type</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>
</fieldset>

fieldset {
    border: 1px solid #ccc !important;
    padding: 10px 12px 12px 12px;
}

legend {
    font-size: 14px;
    font-weight: 600;
    padding: 0 8px;
}