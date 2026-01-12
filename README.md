function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Mudgun_Details) {

            // ✅ MVC already returns JSON object
            var parsedData = result_Mudgun_Details;

            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                tableBody += `<tr data-castno="${parsedData[i].CAST_NO}">`;

                tableBody += `<td>
                    <input name="CAST_NO" class="form-control form-control-lg"
                    value="${parsedData[i].CAST_NO || ''}" readonly />
                </td>`;

                tableBody += `<td>
                    <select name="CLOSURE_MODE" class="form-select form-select-lg">
                        <option value=""></option>
                        <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <div class="input-wrapper">
                        <input type="text" class="form-control form-control-lg clay-input"
                        id="clayInput_${i}"
                        name="MG_CLAY_USED"
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

                tableBody += `<td class="d-flex gap-0">
                    <input name="LOT_NO" style="width:120px;"
                    value="${parsedData[i].LOT_NO || ''}" />
                    <button type="button" class="btn btn-primary btn-sm getLot">::</button>
                </td>`;

                tableBody += `<td>
                    <input name="NO_OF_BAGS" class="form-control form-control-lg"
                    value="${parsedData[i].NO_OF_BAGS || ''}" />
                </td>`;

                tableBody += `<td>
                    <input name="MUDGUN_HOLD_TIME" class="form-control form-control-lg"
                    value="${parsedData[i].MUDGUN_HOLD_TIME || ''}" />
                </td>`;

                tableBody += `<td>
                    <select name="CLAY_LEAKAGE" class="form-select form-select-lg">
                        <option value=""></option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <select name="BACK_FIRE" class="form-select form-select-lg">
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
            console.error(err);
        }
    });
}
