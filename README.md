.scroll-x {
    overflow-x: auto;
    position: relative;
}

/* Freeze CAST_NO column */
#Mudgun_Details th:first-child,
#Mudgun_Details td:first-child {
    position: sticky;
    left: 0;
    background: #ffffff;
    z-index: 5;
    min-width: 130px;
}

/* Header above body */
#Mudgun_Details th:first-child {
    z-index: 6;
    background: #f8f9fa;
}
<div class="table-responsive scroll-x">
    <table id="Mudgun_Details" class="table table-bordered table-sm align-middle">
        <thead class="table-light">
            <tr>
                <th>CAST NO</th>
                <th>CLOSURE MODE</th>
                <th>MG CLAY USED</th>
                <th>LOT NO</th>
                <th>NO OF BAGS</th>
                <th>MUDGUN HOLD TIME</th>
                <th>MUDGUN NOZZLE</th>
                <th>NOZZLE BEF</th>
                <th>NOZZLE AFT</th>
                <th>INIT PRESS</th>
                <th>MAX PRESS</th>
                <th>FINAL PRESS</th>
                <th>PRESS FORCE</th>
                <th>CLAY LEAK</th>
                <th>BACK FIRE</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>
