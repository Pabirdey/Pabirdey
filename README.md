<!-- Scrollable Container 1 -->
<div id="scrollDiv1" style="max-height: 260px; overflow-y: auto; border: 1px solid #ccc;">
    <table id="castTable1" class="table table-bordered table-sm text-center align-middle mb-0">
        <thead class="table-light sticky-top">
            <tr>
                <th>Cast No</th>
                <th>Trough No</th>
                <th>Cast Start</th>
                <th>Duration</th>
                <th>Rate</th>
                <th>TLC</th>
                <th>OT</th>
                <th>Ready Time</th>
                <th>Wetness</th>
                <th>Cast Type</th>
                <th>Clay</th>
                <th>Taphole</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- Scrollable Container 2 -->
<div id="scrollDiv2" style="max-height: 260px; overflow-y: auto; border: 1px solid #ccc;">
    <table id="castTable2" class="table table-bordered table-sm text-center align-middle mb-0">
        <thead class="table-light sticky-top">
            <tr>
                <th>Cast No</th>
                <th>Trough No</th>
                <th>Cast Start</th>
                <th>Duration</th>
                <th>Rate</th>
                <th>TLC</th>
                <th>OT</th>
                <th>Ready Time</th>
                <th>Wetness</th>
                <th>Cast Type</th>
                <th>Clay</th>
                <th>Taphole</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- Scroll Sync Script -->
<script>
    const div1 = document.getElementById('scrollDiv1');
    const div2 = document.getElementById('scrollDiv2');

    let isSyncing1 = false;
    let isSyncing2 = false;

    div1.addEventListener('scroll', () => {
        if (!isSyncing1) {
            isSyncing2 = true;
            div2.scrollTop = div1.scrollTop;
        }
        isSyncing1 = false;
    });

    div2.addEventListener('scroll', () => {
        if (!isSyncing2) {
            isSyncing1 = true;
            div1.scrollTop = div2.scrollTop;
        }
        isSyncing2 = false;
    });
</script>