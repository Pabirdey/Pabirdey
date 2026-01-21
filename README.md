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

    <div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
        <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
            <thead class="table-secondary sticky-top">
                <tr>
                    <th style="width:100px;">ID No</th>
                    <th>Taphole No</th>
                    <th style="width:150px;">Date Time</th>
                    <th style="width:100px;">HH24</th>
                    <th style="width:100px;">MM</th>
                    <th>Taphole Length</th>
                    <th>Clay Paused</th>
                    <th style="width:180px;">Type</th>
                </tr>
            </thead>
            <tbody>
                <!-- rows created by JS -->
            </tbody>
        </table>
    </div>
</fieldset>