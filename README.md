@{
    Layout = null;   /* for testing – remove if using _Layout */
}
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <!-- Bootstrap & jQuery -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <!-- Datepicker -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>

    <style>
        .input-wrapper {
            display: flex;
            border: 1px solid #999;
        }
        .arrow-btn {
            width: 30px;
            cursor: pointer;
            background: #eee;
            text-align: center;
        }
        .list-box {
            display: none;
            position: absolute;
            background: #fff;
            border: 1px solid #999;
            z-index: 9999;
        }
        .list-box div {
            padding: 5px;
            cursor: pointer;
        }
        .list-box div:hover {
            background: #e6e6e6;
        }
    </style>
</head>

<body>

<div class="container mt-4">

    <h2 class="text-center mb-3">Cast House Details</h2>

    <div class="mb-3">
        <label>Date</label>
        <input id="tbFDatePick" class="form-control w-25 d-inline">
        &nbsp;&nbsp;
        <label>Furnace</label>
        <select id="lstFur">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
        </select>
    </div>

    <table class="table table-bordered" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>Closure Mode</th>
                <th>Clay Used</th>
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
                <h5 class="modal-title w-100 text-center">MG CLAY DETAILS</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <div class="mb-3">
                    <label>Clay 1</label>
                    <select class="form-select">
                        <option>Clay A</option>
                        <option>Clay B</option>
                    </select>
                </div>

                <div class="mb-3">
                    <label>Clay 2</label>
                    <select class="form-select">
                        <option>Clay A</option>
                        <option>Clay B</option>
                    </select>
                </div>

                <div class="mb-3">
                    <label>Clay 3</label>
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
<!-- ============== END MODAL ================= -->

<script>
    var activeRowIndex = null;

    $(document).ready(function () {

        $('#tbFDatePick').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true
        });

        // DEMO DATA (replace with AJAX later)
        var data = [
            { CAST_NO: 101, MG_CLAY_USED: "" },
            { CAST_NO: 102, MG_CLAY_USED: "" }
        ];

        renderTable(data);
    });

    function renderTable(data) {

        var html = "";

        for (var i = 0; i < data.length; i++) {

            html += `
<tr>
<td>${data[i].CAST_NO}</td>

<td>
<select class="form-select">
<option>MUDGUN</option>
<option>NULL</option>
</select>
</td>

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

        $("#Mudgun_Details tbody").html(html);
    }

    function toggleList(index) {
        $("#list_" + index).toggle();
    }

    function selectItem(el, index) {

        $("#clayInput_" + index).val(el.innerText);
        $("#list_" + index).hide();

        if (el.innerText === "OTHERS") {
            activeRowIndex = index;
            bootstrap.Modal.getOrCreateInstance(
                document.getElementById("clayModal")
            ).show();
        }
    }

    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper") &&
            !e.target.closest(".list-box")) {
            $(".list-box").hide();
        }
    });
</script>

</body>
</html>
