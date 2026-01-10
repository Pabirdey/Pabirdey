[HttpGet]
    public ActionResult Get_Display_Mudgun_Details(string Fdate, string Fur)
    {
        var data = new[]
        {
            new { CAST_NO = 101, MG_CLAY_USED = "" },
            new { CAST_NO = 102, MG_CLAY_USED = "" },
            new { CAST_NO = 103, MG_CLAY_USED = "" }
        };

        return Json(JsonConvert.SerializeObject(data),
                    JsonRequestBehavior.AllowGet);
    }
}
@{
    ViewBag.Title = "Mudgun Details";
    Layout = null;
}

<!DOCTYPE html>
<html>
<head>
    <title>Mudgun</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" />
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        .input-wrapper {
            display: flex;
            position: relative;
        }
        .arrow-btn {
            width: 30px;
            background: #eee;
            cursor: pointer;
            text-align: center;
        }
        .list-box {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            background: #fff;
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

    <button class="btn btn-primary mb-3"
            onclick="Display_Mudgun_Details('01-01-2026','BF1')">
        Load Mudgun Details
    </button>

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
                    Clay 1
                    <select id="clay1" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                        <option>CLAY C</option>
                    </select>
                </div>

                <div class="mb-2">
                    Clay 2
                    <select id="clay2" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                        <option>CLAY C</option>
                    </select>
                </div>

                <div class="mb-2">
                    Clay 3
                    <select id="clay3" class="form-select">
                        <option value="">Select</option>
                        <option>CLAY A</option>
                        <option>CLAY B</option>
                        <option>CLAY C</option>
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
let currentRowIndex = -1;

// ================= AJAX LOAD =================
function Display_Mudgun_Details(Fdate, Fur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
        type: 'GET',
        data: { Fdate: Fdate, Fur: Fur },
        success: function (result) {

            var parsedData = JSON.parse(result);
            var html = "";

            for (var i = 0; i < parsedData.length; i++) {

                html += `
                <tr>
                    <td>
                        <input class="form-control"
                               value="${parsedData[i].CAST_NO}" readonly />
                    </td>

                    <td>
                        <div class="input-wrapper">
                            <input class="form-control"
                                   id="clayInput_${i}"
                                   value="${parsedData[i].MG_CLAY_USED || ''}" />

                            <div class="arrow-btn"
                                 onclick="toggleList(${i}, event)">▼</div>

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

// ================= DROPDOWN =================
function toggleList(index, e) {
    e.stopPropagation();
    $(".list-box").hide();
    $("#list_" + index).show();
}

function selectItem(el, index, e) {
    e.stopPropagation();

    let value = el.innerText.trim();
    $("#clayInput_" + index).val(value);
    $("#list_" + index).hide();

    if (value === "OTHERS") {
        currentRowIndex = index;
        $("#clay1,#clay2,#clay3").val("");
        new bootstrap.Modal("#clayModal").show();
    }
}

// ================= MODAL SAVE =================
function saveClay() {

    let arr = [];
    if (clay1.value) arr.push(clay1.value);
    if (clay2.value) arr.push(clay2.value);
    if (clay3.value) arr.push(clay3.value);

    if (arr.length === 0) {
        alert("Select at least one clay");
        return;
    }

    $("#clayInput_" + currentRowIndex).val(arr.join(" + "));
    bootstrap.Modal.getInstance(document.getElementById("clayModal")).hide();
}

// ================= CLICK OUTSIDE =================
document.addEventListener("click", function () {
    $(".list-box").hide();
});
</script>

</body>
</html>
