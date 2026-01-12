<script>
var activeRowIndex = null;

function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result) {

            // ✔ Safe JSON handling
            var parsedData = (typeof result === "string") ? JSON.parse(result) : result;

            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                tableBody += `<tr data-castno="${parsedData[i].CAST_NO}">`;

                tableBody += `<td><input class="form-control" value="${parsedData[i].CAST_NO}" readonly></td>`;

                tableBody += `<td>
                    <select class="form-select">
                        <option value=""></option>
                        <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>`;

                tableBody += `
                <td>
                    <div class="input-wrapper position-relative">
                        <input type="text" class="form-control" id="clayInput_${i}" value="${parsedData[i].MG_CLAY_USED || ''}">
                        <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                    </div>
                    <div class="list-box" id="list_${i}" style="display:none;">
                        <div onclick="selectItem(this,${i})">ACE</div>
                        <div onclick="selectItem(this,${i})">BRL</div>
                        <div onclick="selectItem(this,${i})">LRH</div>
                        <div onclick="selectItem(this,${i})">OTHERS</div>
                    </div>
                </td>`;

                tableBody += `<td>
                    <input value="${parsedData[i].LOT_NO || ''}" style="width:120px;">
                    <button class="btn btn-sm btn-primary">::</button>
                </td>`;

                tableBody += `<td><input class="form-control" value="${parsedData[i].NO_OF_BAGS || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].MUDGUN_HOLD_TIME || ''}"></td>`;

                tableBody += `<td>
                    <select class="form-select">
                        <option></option>
                        <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                        <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                    </select>
                </td>`;

                tableBody += `<td><input class="form-control" value="${parsedData[i].MNOZZLE_BEF_CLOSING || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].MNOZZLE_AFT_CLOSING || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].INIT_PLUGIN_PRESSURE || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].MAX_PLUGIN_PRESSURE || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].FINAL_PLUGIN_PRESSURE || ''}"></td>`;
                tableBody += `<td><input class="form-control" value="${parsedData[i].PRESS_ON_FORCE || ''}"></td>`;

                tableBody += `<td>
                    <select class="form-select">
                        <option></option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <select class="form-select">
                        <option></option>
                        <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                tableBody += `</tr>`;
            }

            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
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

function saveOtherClay() {
    $("#clayInput_" + activeRowIndex).val($("#otherClay").val());
    bootstrap.Modal.getInstance(document.getElementById("clayModal")).hide();
}

document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") && !e.target.closest(".list-box")) {
        $(".list-box").hide();
    }
});
</script>
