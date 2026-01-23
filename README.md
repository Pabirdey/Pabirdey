<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Datepicker -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">

    <style>
        .scrollable-table {
            max-height: 318px;
            overflow-x: auto;
            overflow-y: auto;
            position: relative;
        }

        /* Freeze Cast No column */
        #Mudgun_Details th:first-child,
        #Mudgun_Details td:first-child {
            position: sticky;
            left: 0;
            background: #fff;
            z-index: 5;
            min-width: 120px;
        }

        /* Sticky header */
        #Mudgun_Details thead th {
            position: sticky;
            top: 0;
            z-index: 4;
            background: #343a40;
            color: white;
        }

        .input-wrapper {
            position: relative;
        }

        .arrow-btn {
            position: absolute;
            right: 8px;
            top: 8px;
            cursor: pointer;
            user-select: none;
        }

        .list-box {
            display: none;
            position: absolute;
            background: #fff;
            border: 1px solid #ccc;
            width: 100%;
            max-height: 200px;
            overflow-y: auto;
            z-index: 9999;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #f0f0f0;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-2">

    <h2 class="text-center mb-3">Cast House Details</h2>

    <!-- Date & Furnace -->
    <div class="mb-3">
        <input id="tbFDatePick" style="width:140px;text-align:center" />
        <select id="lstFur">
            <option value="">Select Furnace</option>
            <option>C</option><option>E</option><option>F</option>
            <option>G</option><option>H</option><option>I</option>
        </select>
    </div>

    <!-- Mudgun Details -->
    <div class="form-section">
        <h5>Mudgun Details</h5>

        <div class="table-responsive scrollable-table">
            <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                <thead>
                    <tr>
                        <th>Cast No</th>
                        <th>Closure Mode</th>
                        <th>Clay Qty</th>
                        <th>MG Clay Type</th>
                        <th>Back Fire</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

</div>

<!-- ================= MODAL ================= -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header">
                <h5 class="modal-title">Other MG Clay Type</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <input type="hidden" id="hdnRowIndex" />
                <input type="text"
                       id="txtOtherMGClay"
                       class="form-control form-control-lg"
                       placeholder="Enter MG Clay Type">
            </div>

            <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
            </div>

        </div>
    </div>
</div>

<!-- JS -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

<script>
let lsSelectedFDate = '';
let IsSelectedFur = '';

$(document).ready(function () {

    lsSelectedFDate = '@DateTime.Today.ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

    $('#tbFDatePick').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true
    }).val(lsSelectedFDate);

    $('#tbFDatePick, #lstFur').on('change', function () {
        IsSelectedFur = $('#lstFur').val();
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
    });

    Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
});

/* ================= DISPLAY TABLE ================= */
function Display_Mudgun_Details(fdate, fur) {

    // DEMO DATA (replace with AJAX result)
    let data = [
        { CAST_NO: 1 },
        { CAST_NO: 2 },
        { CAST_NO: 3 }
    ];

    let html = '';

    for (let i = 0; i < data.length; i++) {

        html += `
        <tr>
            <td>
                <input class="form-control" value="${data[i].CAST_NO}" readonly>
            </td>

            <td>
                <select class="form-select">
                    <option></option>
                    <option>MUDGUN</option>
                    <option>NULL</option>
                </select>
            </td>

            <td>
                <input class="form-control">
            </td>

            <td>
                <select class="form-select"
                        onchange="onMGClayChange(this, ${i})">
                    <option></option>
                    <option>ACE</option>
                    <option>BRL</option>
                    <option>LRH</option>
                    <option>OTHERS</option>
                </select>
            </td>

            <td>
                <select class="form-select">
                    <option></option>
                    <option>YES</option>
                    <option>NO</option>
                </select>
            </td>
        </tr>`;
    }

    $("#Mudgun_Details tbody").html(html);
}

/* ================= OPEN MODAL ================= */
function onMGClayChange(ctrl, rowIndex) {

    if (ctrl.value === "OTHERS") {

        $("#hdnRowIndex").val(rowIndex);
        $("#txtOtherMGClay").val("");

        let modal = new bootstrap.Modal(
            document.getElementById("mgClayOtherModal")
        );
        modal.show();
    }
}

/* ================= SAVE MODAL VALUE ================= */
function saveOtherMGClay() {

    let rowIndex = $("#hdnRowIndex").val();
    let val = $("#txtOtherMGClay").val().trim();

    if (val === '') {
        alert("Enter MG Clay Type");
        return;
    }

    let row = $("#Mudgun_Details tbody tr").eq(rowIndex);
    let select = row.find("select").eq(1);

    select.append(`<option selected>${val}</option>`);

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}
</script>

</body>
</html>
