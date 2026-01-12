function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },

        success: function (result_Mudgun_Details) {

            // ✅ MVC already gives JSON object
            var parsedData = result_Mudgun_Details;
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                tableBody += `<tr data-castno="${parsedData[i].CAST_NO}">`;

                tableBody += `<td>
                    <input class="form-control form-control-lg"
                           value="${parsedData[i].CAST_NO || ''}" readonly />
                </td>`;

                tableBody += `<td>
                    <select class="form-select form-select-lg">
                        <option value=""></option>
                        <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <div class="input-wrapper">
                        <input type="text"
                               class="form-control form-control-lg clay-input"
                               id="clayInput_${i}"
                               value="${parsedData[i].MG_CLAY_USED || ''}">
                        <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                    </div>

                    <div class="list-box" id="list_${i}">
                        <div onclick="selectItem(this, ${i})">ACE</div>
                        <div onclick="selectItem(this, ${i})">BRL</div>
                        <div onclick="selectItem(this, ${i})">LRH</div>
                        <div onclick="selectItem(this, ${i})">UBQ</div>
                        <div onclick="selectItem(this, ${i})">SARVESH</div>
                        <div onclick="selectItem(this, ${i})">OTHERS</div>
                    </div>
                </td>`;

                tableBody += `<td>
                    <input class="form-control form-control-lg"
                           value="${parsedData[i].NO_OF_BAGS || ''}">
                </td>`;

                tableBody += `<td>
                    <input class="form-control form-control-lg"
                           value="${parsedData[i].MUDGUN_HOLD_TIME || ''}">
                </td>`;

                tableBody += `<td>
                    <select class="form-select form-select-lg">
                        <option value=""></option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <select class="form-select form-select-lg">
                        <option value=""></option>
                        <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                tableBody += `</tr>`;
            }

            $("#Mudgun_Details tbody").html(tableBody);
        },

        error: function (err) {
            console.error("Mudgun error:", err);
        }
    });
}

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
<script>
    var activeRowIndex = null;

    function toggleList(index) {
        $(".list-box").hide(); // close others
        $("#list_" + index).toggle();
    }

    function selectItem(el, index) {
        $("#clayInput_" + index).val(el.innerText);
        $("#list_" + index).hide();

        if (el.innerText === "OTHERS") {
            activeRowIndex = index;
            var modal = bootstrap.Modal.getOrCreateInstance(
                document.getElementById("clayModal")
            );
            modal.show();
        }
    }

    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper") && !e.target.closest(".list-box")) {
            $(".list-box").hide();
        }
    });
</script>

