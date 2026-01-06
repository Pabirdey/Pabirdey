<fieldset class="border rounded p-3 shadow-sm">
    <legend class="float-none w-auto px-2">
        Carbon Paste Inj
    </legend>

    <div class="d-flex justify-content-between align-items-center mb-2">
        <span></span>
        <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">Save</button>
    </div>

    <div class="table-responsive scrollable-table" style="max-height:255px;">
        <table class="table table-bordered table-sm text-center align-middle" id="carbon_paste_inj">
            <thead>
                <tr>
                    <th class="Heading_Small">Date Time</th>
                    <th class="Heading_Small">Shift</th>
                    <th class="Heading_Small">Below Tuyere</th>
                    <th class="Heading_Small">No of Drum</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>
</fieldset>

fieldset {
    border: 1px solid #ccc !important;
    padding: 10px;
}

legend {
    font-size: 14px;
    font-weight: 600;
}