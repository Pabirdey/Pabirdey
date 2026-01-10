<!DOCTYPE html>
<html>
<head>
    <title>Mudgun Details</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        .input-wrapper {
            display: flex;
            position: relative;
        }
        .arrow-btn {
            width: 30px;
            cursor: pointer;
            text-align: center;
            background: #eee;
        }
        .list-box {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            background: white;
            border: 1px solid #ccc;
            display: none;
            z-index: 999;
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

<div class="container mt-4">
    <table class="table table-bordered" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>MG Clay Used</th>
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
                <h5 class="modal-title w-100 text-center">Clay Weightage</h5>
                <button class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <div class="mb-2">
                    Clay1
                    <select id="clay1" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                    </select>
                </div>

                <div class="mb-2">
                    Clay2
                    <select id="clay2" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                    </select>
                </div>

                <div class="mb-2">
                    Clay3
                    <select id="clay3" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                    </select>
                </div>
            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" onclick="saveClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>
<script>
function Display_Mudgun_Details(Fdate, Fur) {

    $.ajax({
        url: '/CastHouse/Get_Display_Mudgun_Details',
        type: 'GET',
        data: { Fdate: Fdate, Fur: Fur },
        success: function (result) {

            var parsedData = JSON.parse(result);
            var html = "";

            for (var i = 0; i < parsedData.length; i++) {

                html += `
                <tr>
                    <td>
                        <input class="form-control" value="${parsedData[i].CAST_NO}" readonly>
                    </td>

                    <td>
                        <div class="input-wrapper">
                            <input type="text" class="form-control"
                                   id="clayInput_${i}"
                                   value="${parsedData[i].MG_CLAY_USED || ''}">

                            <div class="arrow-btn" onclick="toggleList(${i}, event)">▼</div>

                            <div class="list-box" id="list_${i}">
                                <div onclick="selectItem(this, ${i}, event)">ACE</div>
                                <div onclick="selectItem(this, ${i}, event)">BRL</div>
                                <div onclick="selectItem(this, ${i}, event)">LRH</div>
                                <div onclick="selectItem(this, ${i}, event)">OTHERS</div>
                            </div>
                        </div>
                    </td>
                </tr>`;
            }

            $("#Mudgun_Details tbody").html(html);
        }
    });
}
</script>
<script>
let currentRowIndex = -1;

function toggleList(index, e) {
    e.stopPropagation();
    $(".list-box").hide();
    $("#list_" + index).show();
}

function selectItem(el, index, e) {
    e.stopPropagation();

    var val = el.innerText.trim();
    $("#clayInput_" + index).val(val);
    $("#list_" + index).hide();

    if (val === "OTHERS") {
        currentRowIndex = index;
        $("#clay1,#clay2,#clay3").val("");
        new bootstrap.Modal("#clayModal").show();
    }
}

function saveClay() {

    var result = [];
    if (clay1.value) result.push(clay1.value);
    if (clay2.value) result.push(clay2.value);
    if (clay3.value) result.push(clay3.value);

    if (result.length === 0) {
        alert("Select at least one clay");
        return;
    }

    $("#clayInput_" + currentRowIndex).val(result.join(" + "));
    bootstrap.Modal.getInstance(document.getElementById("clayModal")).hide();
}

document.addEventListener("click", function () {
    $(".list-box").hide();
});
</script>

</body>
</html>
