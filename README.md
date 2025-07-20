<style>
    .scrollable-tbody {
        display: block;
        max-height: 210px; /* Adjust based on row height */
        overflow-y: auto;
    }

    .scrollable-tbody tr {
        display: table;
        width: 100%;
        table-layout: fixed;
    }

    .table thead,
    .table tbody tr {
        display: table;
        width: 100%;
        table-layout: fixed;
    }
</style>

<div class="row align-items-stretch">
    <!-- Tap Hole Details -->
    <div class="col-md-8 d-flex">
        <div class="card w-100">
            <div class="card-header bg-primary text-white">Tap Hole Details</div>
            <div class="card-body table-responsive" style="overflow-x:auto;">
                <table class="table table-bordered text-center align-middle" style="min-width:1200px;">
                    <thead class="table-light">
                        <tr>
                            <th>Cast No</th>
                            <th>Trough</th>
                            <th>Cast Start</th>
                            <th>Cast End</th>
                            <th>Gutko</th>
                            <th class="long-header">Cast Duration</th>
                            <th class="long-header">Casting Rate(t/min)</th>
                            <th>TLC</th>
                            <th>OT</th>
                            <th class="long-header">Cast Ready Time</th>
                            <th class="long-header">Splashing Wetness Time</th>
                            <th class="long-header">Cast Type</th>
                            <th class="long-header">Clay Condition</th>
                            <th class="long-header">Taphole Behaviour at End Cast</th>
                        </tr>
                    </thead>
                    <tbody class="scrollable-tbody">
                        <!-- Sample rows -->
                        <tr><td colspan="14">Row 1</td></tr>
                        <tr><td colspan="14">Row 2</td></tr>
                        <tr><td colspan="14">Row 3</td></tr>
                        <tr><td colspan="14">Row 4</td></tr>
                        <tr><td colspan="14">Row 5</td></tr>
                        <tr><td colspan="14">Row 6</td></tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Hot Metal Details -->
    <div class="col-md-4 d-flex">
        <div class="card w-100">
            <div class="card-header bg-secondary text-white">Hot Metal Details</div>
            <div class="card-body table-responsive">
                <table class="table table-bordered table-sm text-center">
                    <thead class="table-light">
                        <tr>
                            <th class="long-header">HMT Before Slag</th>
                            <th class="long-header">HMT After Slag</th>
                            <th>Final HM Temp</th>
                            <th>HM Weight</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Sample rows -->
                        <tr><td colspan="4">HM 1</td></tr>
                        <tr><td colspan="4">HM 2</td></tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</div>
