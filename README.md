<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>
    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Datepicker -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">       
    <style>
        body { font-family: "Courier New", Courier, monospace; }
        .table-input { font-size: 1rem; padding: 2px 4px; border: 2px solid; }
        .scrollable-table { max-height: 318px; overflow-x:auto; overflow-y:auto; position:relative; }
        #Mudgun_Details th:first-child,
        #Mudgun_Details td:first-child { position: sticky; left:0; background:#fff; z-index:3; min-width:120px; }
        #Mudgun_Details thead th:first-child { background:#f8f9fa; z-index:5; }
        th { font-family: Courier New; font-weight:bold; border:1px solid; color:white; }
        .Long_Heading_Medium { min-width: 100px; border:1px solid black; }
        .form-section { background:#fff; padding:20px; border-radius:20px; box-shadow:0 10px 20px rgba(0,0,0,0.1); margin-bottom:25px; }
        .section-title { background:#EEB86D; color:black; padding:5px 10px; margin-bottom:10px; font-weight:bold; border-radius:10px; font-size:18px; }
        .form-control-lg { font-size:1.2rem; color:black; }
        .input-wrapper { position:relative; display:flex; border:1px solid #999; }
        .input-wrapper input { border:none; outline:none; flex:1; }
        .arrow-btn { position:absolute; right:5px; top:5px; cursor:pointer; user-select:none; background:#f0f0f0; width:25px; text-align:center; }
        .list-box { display:none; position:absolute; background:white; border:1px solid #ccc; width:100%; max-height:200px; overflow-y:auto; z-index:9999; }
        .list-box div { padding:6px; cursor:pointer; }
        .list-box div:hover { background:#f0f0f0; }
        .Main-Heading { font-family:Allan,cursive; font-weight:bold; font-size:6vh; text-align:center; padding:20px; color:#393939; }
    </style>
</head>
<body>
<div class="Main-Heading mt-0">Cast House Details</div>

<div class="container-fluid mt-0">
    <div class="form-group">
        <label for="tbFDatePick" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
        <input id="tbFDatePick" size="14" style="height:28px;text-align:center">
        &nbsp;&nbsp;&nbsp;&nbsp;
        <label style="font-family:Allan,cursive;font-size:25px;">Furnace</label>
        <select id="lstFur">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <!-- Mudgun Details -->
    <div class="form-section">
        <div class="section-title">Mudgun Details</div>
        <div class="table-responsive scrollable-table" style="max-height:318px;">
            <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                <thead>
                    <tr>
                        <th class="Long_Heading_Medium">Cast No</th>
                        <th>Closure Mode</th>
                        <th>Clay Qty. Pushed</th>
                        <th>MG Clay Type</th>
                        <th>Lot No</th>
                        <th>No. of Bags</th>
                        <th>Mudgun Holding Time</th>
                        <th>Mudgun Nozzle</th>
                        <th>M.Nozzle Temp Before Closing</th>
                        <th>M.Nozzle Temp after Closing</th>
                        <th>Initial Plugin Pressure</th>
                        <th>Max Plugin Pressure</th>
                        <th>Final Plugin Pressure</th>
                        <th>Pressure On Force</th>
                        <th>Clay Leakage</th>
                        <th>Back Fire</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<!-- Modal for Other MG Clay -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Other MG Clay Type</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <input type="hidden" id="hdnRowIndex" />
                <input type="text" id="txtOtherMGClay" class="form-control form-control-lg" placeholder="Enter MG Clay Type">
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
            </div>
        </div>
    </div>
</div>

<!-- Scripts -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>
<script>
let lsSelectedFDate;
let IsSelectedFur;

$(document).ready(function () {
    lsSelectedFDate = new Date().toLocaleDateString('en-GB');
    $('#tbFDatePick').datepicker({ format: "dd/mm/yyyy", autoclose:true, todayHighlight:true }).val(lsSelectedFDate);

    $('#tbFDatePick').on('changeDate', function () {
        lsSelectedFDate = $(this).val();
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
    });

    $('#lstFur').change(function () {
        IsSelectedFur = $(this).val();
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
    });

    Display_Mudgun_Details(lsSelectedFDate, $('#lstFur').val());
});

// Toggle dropdown list
function toggleList(i) {
    $(".list-box").hide();
    $("#list_" + i).toggle();
}

// Select item from list
function selectItem(el, rowIndex) {
    let value = el.innerText.trim();
    if (value === "OTHERS") {
        $("#hdnRowIndex").val(rowIndex);
        $("#txtOtherMGClay").val("");
        let modalEl = document.getElementById("mgClayOtherModal");
        let modal = bootstrap.Modal.getInstance(modalEl) || new bootstrap.Modal(modalEl);
        modal.show();
        return;
    }
    $("#clayInput_" + rowIndex).val(value);
    $("#list_" + rowIndex).hide();
}

// Save Other MG Clay from modal
function saveOtherMGClay() {
    let rowIndex = $("#hdnRowIndex").val();
    let val = $("#txtOtherMGClay").val().trim();
    if(!val){ alert("Please enter MG Clay Type"); return; }
    $("#clayInput_" + rowIndex).val(val);
    let modalEl = document.getElementById("mgClayOtherModal");
    let modal = bootstrap.Modal.getInstance(modalEl);
    if(modal) modal.hide();
}

// Display Mudgun Details
function Display_Mudgun_Details(date, fur) {
    // Mock AJAX Data
    let parsedData = [
        { CAST_NO: "C001", CLOSURE_MODE:"MUDGUN", CLAY_QUANTITY: 10, LOT_NO:"L01", NO_OF_BAGS:5, MUDGUN_HOLD_TIME:3, MUDGUN_NOZZLE:"REPLACEMENT", MNOZZLE_BEF_CLOSING:50, MNOZZLE_AFT_CLOSING:55, INIT_PLUGIN_PRESSURE:100, MAX_PLUGIN_PRESSURE:120, FINAL_PLUGIN_PRESSURE:110, PRESS_ON_FORCE:200, CLAY_LEAKAGE:"NO", BACK_FIRE:"NO" },
        { CAST_NO: "C002", CLOSURE_MODE:"NULL", CLAY_QUANTITY: 15, LOT_NO:"L02", NO_OF_BAGS:6, MUDGUN_HOLD_TIME:4, MUDGUN_NOZZLE:"WEILD", MNOZZLE_BEF_CLOSING:52, MNOZZLE_AFT_CLOSING:57, INIT_PLUGIN_PRESSURE:105, MAX_PLUGIN_PRESSURE:125, FINAL_PLUGIN_PRESSURE:115, PRESS_ON_FORCE:205, CLAY_LEAKAGE:"YES", BACK_FIRE:"YES" }
    ];

    let tableBody = "";
    parsedData.forEach((d,i)=>{
        tableBody += `<tr data-castno='${d.CAST_NO}'>`;
        tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${d.CAST_NO}' readonly/></td>`;
        tableBody += `<td>
            <select name="CLOSURE_MODE" class='form-select form-select-lg'>
                <option ${!d.CLOSURE_MODE?'selected':''}></option>
                <option ${d.CLOSURE_MODE==="MUDGUN"?'selected':''}>MUDGUN</option>
                <option ${d.CLOSURE_MODE==="NULL"?'selected':''}>NULL</option>
            </select>
        </td>`;
        tableBody += `<td><input name="CLAY_QUANTITY" class='form-control form-control-lg' value='${d.CLAY_QUANTITY}'/></td>`;

        // MG Clay Type input + dropdown
        tableBody += `<td>
            <div class="input-wrapper">
                <input type="text" class="form-control form-control-lg" id="clayInput_${i}" name="MG_CLAY_USED" readonly>
                <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                <div class="list-box" id="list_${i}">
                    <div onclick="selectItem(this, ${i})">ACE</div>
                    <div onclick="selectItem(this, ${i})">BRL</div>
                    <div onclick="selectItem(this, ${i})">LRH</div>
                    <div onclick="selectItem(this, ${i})">UBQ</div>
                    <div onclick="selectItem(this, ${i})">SARVESH</div>
                    <div onclick="selectItem(this, ${i})">OTHERS</div>
                </div>
            </div>
        </td>`;

        tableBody += `<td><input name="LOT_NO" class='form-control form-control-lg' value='${d.LOT_NO}'/></td>`;
        tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-lg' value='${d.NO_OF_BAGS}'/></td>`;
        tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-lg' value='${d.MUDGUN_HOLD_TIME}'/></td>`;
        tableBody += `<td>
            <select name="MUDGUN_NOZZLE" class='form-select form-select-lg'>
                <option ${!d.MUDGUN_NOZZLE?'selected':''}></option>
                <option ${d.MUDGUN_NOZZLE==="REPLACEMENT"?'selected':''}>REPLACEMENT</option>
                <option ${d.MUDGUN_NOZZLE==="WEILD"?'selected':''}>WEILD</option>
            </select>
        </td>`;
        tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-lg' value='${d.MNOZZLE_BEF_CLOSING}'/></td>`;
        tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-lg' value='${d.MNOZZLE_AFT_CLOSING}'/></td>`;
        tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${d.INIT_PLUGIN_PRESSURE}'/></td>`;
        tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${d.MAX_PLUGIN_PRESSURE}'/></td>`;
        tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${d.FINAL_PLUGIN_PRESSURE}'/></td>`;
        tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-lg' value='${d.PRESS_ON_FORCE}'/></td>`;
        tableBody += `<td>
            <select name="CLAY_LEAKAGE" class='form-select form-select-lg'>
                <option ${!d.CLAY_LEAKAGE?'selected':''}></option>
                <option ${d.CLAY_LEAKAGE==="YES"?'selected':''}>YES</option>
                <option ${d.CLAY_LEAKAGE==="NO"?'selected':''}>NO</option>
            </select>
        </td>`;
        tableBody += `<td>
            <select name="BACK_FIRE" class='form-select form-select-lg'>
                <option ${!d.BACK_FIRE?'selected':''}></option>
                <option ${d.BACK_FIRE==="YES"?'selected':''}>YES</option>
                <option ${d.BACK_FIRE==="NO"?'selected':''}>NO</option>
            </select>
        </td>`;
        tableBody += `</tr>`;
    });

    $("#Mudgun_Details tbody").html(tableBody);
}
</script>
</body>
</html>
