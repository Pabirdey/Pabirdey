@{
    ViewBag.Title = "Cast House Details";
}

<!DOCTYPE html>
<html>
<head>
    <title>Cast House Details</title>

    <!-- CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- JS -->
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

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

<div class="container-fluid mt-3">
    <h3 class="text-center">Mudgun Details</h3>

    <table class="table table-bordered text-center" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>MG Clay Type</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- ================= MODAL ================= -->
<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title w-100 text-center">MG CLAY</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <div class="mb-2">
                    <label>Clay 1</label>
                    <select class="form-select">
                        <option>Clay A</option>
                        <option>Clay B</option>
                    </select>
                </div>
                <div class="mb-2">
                    <label>Clay 2</label>
                    <select class="form-select">
                        <option>Clay A</option>
                        <option>Clay B</option>
                    </select>
                </div>
            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" data-bs-dismiss="modal">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>

<script>
/* ================= GLOBAL FUNCTIONS ================= */

var activeRowIndex = null;

/* DEMO AJAX CALL */
$(document).ready(function () {
    Display_Mudgun_Details();
});

function Display_Mudgun_Details() {

    // Simulating AJAX result
    var parsedData = [
        { CAST_NO: 101, MG_CLAY_USED: "" },
        { CAST_NO: 102, MG_CLAY_USED: "" }
    ];

    var tableBody = "";

    for (var i = 0; i < parsedData.length; i++) {

        tableBody += `
<tr>
<td>${parsedData[i].CAST_NO}</td>
<td>
<div class="input-wrapper">
<input type="text" id="clayInput_${i}" class="form-control">
<div class="arrow-btn" onclick="toggleList(${i})">▼</div>
</div>

<div class="list-box" id="list_${i}">
<div onclick="selectItem(this, ${i})">ACE</div>
<div onclick="selectItem(this, ${i})">BRL</div>
<div onclick="selectItem(this, ${i})">OTHERS</div>
</div>
</td>
</tr>`;
    }

    $("#Mudgun_Details tbody").html(tableBody);
}

function toggleList(index) {
    $("#list_" + index).toggle();
}

function selectItem(el, index) {

    $("#clayInput_" + index).val(el.innerText);
    $("#list_" + index).hide();

    if (el.innerText.trim() === "OTHERS") {
        activeRowIndex = index;

        bootstrap.Modal
            .getOrCreateInstance(document.getElementById("clayModal"))
            .show();
    }
}

// close dropdown on outside click
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {
        $(".list-box").hide();
    }
});
</script>

</body>
</html>
