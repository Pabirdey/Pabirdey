@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>Cast House Details</title>

    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <!-- Bootstrap Datepicker (ONLY ONCE) -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>

    <style>
        .input-wrapper { display:flex; border:1px solid #999 }
        .arrow-btn { width:30px; cursor:pointer; background:#eee; text-align:center }
        .list-box {
            display:none; position:absolute; background:#fff;
            border:1px solid #999; z-index:9999
        }
        .list-box div { padding:5px; cursor:pointer }
        .list-box div:hover { background:#e6e6e6 }
    </style>
</head>

<body>

<div class="container mt-3">
    <label>Date:</label>
    <input id="tbFDatePick" class="form-control w-25">

    <table class="table table-bordered mt-3" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>MG Clay</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- MODAL -->
<div class="modal fade" id="clayModal">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title">MG Clay Details</h5>
                <button class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <select class="form-select mb-2">
                    <option>Clay A</option>
                    <option>Clay B</option>
                </select>
                <select class="form-select">
                    <option>Clay A</option>
                    <option>Clay B</option>
                </select>
            </div>
        </div>
    </div>
</div>

<script>
/* ============ GLOBAL FUNCTIONS ============ */
var activeRowIndex = null;

function toggleList(index) {
    $("#list_" + index).toggle();
}

function selectItem(el, index) {
    $("#clayInput_" + index).val(el.innerText);
    $("#list_" + index).hide();

    if (el.innerText.trim() === "OTHERS") {
        bootstrap.Modal
            .getOrCreateInstance(document.getElementById("clayModal"))
            .show();
    }
}

/* ============ DOCUMENT READY ============ */
$(document).ready(function () {

    // DATEPICKER ✅
    $('#tbFDatePick').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    });

    // DEMO AJAX DATA
    var data = [
        { CAST_NO: 101 },
        { CAST_NO: 102 }
    ];

    var html = "";
    for (var i = 0; i < data.length; i++) {
        html += `
<tr>
<td>${data[i].CAST_NO}</td>
<td>
<div class="input-wrapper">
<input id="clayInput_${i}" class="form-control">
<div class="arrow-btn" onclick="toggleList(${i})">▼</div>
</div>
<div class="list-box" id="list_${i}">
<div onclick="selectItem(this, ${i})">ACE</div>
<div onclick="selectItem(this, ${i})">OTHERS</div>
</div>
</td>
</tr>`;
    }
    $("#Mudgun_Details tbody").html(html);
});

// Close dropdown
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {
        $(".list-box").hide();
    }
});
</script>

</body>
</html>
