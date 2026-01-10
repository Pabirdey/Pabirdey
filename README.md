@{
    Layout = null;
}

<!DOCTYPE html>
<html>
<head>
    <title>Cast House – Mudgun</title>

    <!-- ✅ Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        .input-wrapper {
            display: flex;
            border: 1px solid #999;
            position: relative;
        }

        .input-wrapper input {
            border: none;
            outline: none;
            width: 100%;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            background: white;
            border: 1px solid #999;
            display: none;
            z-index: 1000;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #e6e6e6;
        }
    </style>
</head>

<body class="p-4">

    <h3 class="mb-3">Mudgun Details</h3>

    <table class="table table-bordered" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>MG Clay Type</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <!-- 🔥 MODAL -->
    <div class="modal fade" id="clayModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">

                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>

                <div class="modal-body">
                    <div class="fw-bold text-center mb-3">Weightage of Clay</div>

                    <div class="row mb-2">
                        <div class="col-3">Clay1</div>
                        <div class="col-9">
                            <select class="form-select" id="clay1">
                                <option value="">Select</option>
                                <option>Clay A</option>
                                <option>Clay B</option>
                                <option>Clay C</option>
                            </select>
                        </div>
                    </div>

                    <div class="row mb-2">
                        <div class="col-3">Clay2</div>
                        <div class="col-9">
                            <select class="form-select" id="clay2">
                                <option value="">Select</option>
                                <option>Clay A</option>
                                <option>Clay B</option>
                                <option>Clay C</option>
                            </select>
                        </div>
                    </div>

                    <div class="row">
                        <div class="col-3">Clay3</div>
                        <div class="col-9">
                            <select class="form-select" id="clay3">
                                <option value="">Select</option>
                                <option>Clay A</option>
                                <option>Clay B</option>
                                <option>Clay C</option>
                            </select>
                        </div>
                    </div>
                </div>

                <div class="modal-footer justify-content-center">
                    <button class="btn btn-success" onclick="saveClay()">Save</button>
                    <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>

    <!-- ✅ Bootstrap 5 JS (ONLY ONE) -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

    <script>
        // 🔹 DEMO DATA (simulate AJAX)
        var parsedData = [
            { CAST_NO: "101", MG_CLAY_USED: "" },
            { CAST_NO: "102", MG_CLAY_USED: "" }
        ];

        // 🔹 LOAD TABLE
        function loadTable() {
            let html = "";
            for (let i = 0; i < parsedData.length; i++) {
                html += `
                <tr>
                    <td>${parsedData[i].CAST_NO}</td>
                    <td>
                        <div class="input-wrapper">
                            <input type="text" id="clayInput_${i}" readonly>
                            <div class="arrow-btn" onclick="toggleList(${i})">▼</div>

                            <div class="list-box" id="list_${i}">
                                <div onclick="selectItem(this, ${i})">ACE</div>
                                <div onclick="selectItem(this, ${i})">BRL</div>
                                <div onclick="selectItem(this, ${i})">LRH</div>
                                <div onclick="selectItem(this, ${i})">OTHERS</div>
                            </div>
                        </div>
                    </td>
                </tr>`;
            }
            document.querySelector("#Mudgun_Details tbody").innerHTML = html;
        }

        loadTable();

        // 🔹 TOGGLE LIST
        function toggleList(index) {
            document.getElementById("list_" + index).style.display = "block";
        }

        // 🔹 SELECT ITEM
        function selectItem(el, index) {

            document.getElementById("clayInput_" + index).value = el.innerText;
            document.getElementById("list_" + index).style.display = "none";

            if (el.innerText === "OTHERS") {
                window.currentRowIndex = index;

                let modal = bootstrap.Modal.getOrCreateInstance(
                    document.getElementById("clayModal")
                );
                modal.show();
            }
        }

        // 🔹 SAVE CLAY
        function saveClay() {

            alert(
                "Row: " + window.currentRowIndex +
                "\nClay1: " + clay1.value +
                "\nClay2: " + clay2.value +
                "\nClay3: " + clay3.value
            );

            bootstrap.Modal.getInstance(
                document.getElementById("clayModal")
            ).hide();
        }

        // 🔹 CLOSE LIST WHEN CLICK OUTSIDE
        document.addEventListener("click", function (e) {
            if (!e.target.closest(".input-wrapper")) {
                document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");
            }
        });
    </script>

</body>
</html>
