function Display_Mudgun_Details(date, furnace) {
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
        type: 'GET',
        data: { Fdate: date, Fur: furnace },
        success: function (result) {

            let parsedData = JSON.parse(result);
            let tableBody = "";

            for (let i = 0; i < parsedData.length; i++) {

                tableBody += `
                <tr data-castno="${parsedData[i].CAST_NO}">
                    <td class="freeze-col">
                        ${parsedData[i].CAST_NO}
                        <input type="hidden" name="CAST_NO" value="${parsedData[i].CAST_NO}">
                    </td>

                    <td>
                        <select name="CLOSURE_MODE" class="form-select form-select-sm">
                            <option value=""></option>
                            <option value="MUDGUN" ${parsedData[i].CLOSURE_MODE === "MUDGUN" ? "selected" : ""}>MUDGUN</option>
                            <option value="NULL" ${parsedData[i].CLOSURE_MODE === "NULL" ? "selected" : ""}>NULL</option>
                        </select>
                    </td>

                    <td><input name="CLAY_QUANTITY" class="form-control form-control-sm" value="${parsedData[i].CLAY_QUANTITY || ''}"></td>
                    <td><input name="MG_CLAY_USED" class="form-control form-control-sm" value="${parsedData[i].MG_CLAY_USED || ''}"></td>
                    <td><input name="LOT_NO" class="form-control form-control-sm" value="${parsedData[i].LOT_NO || ''}"></td>
                    <td><input name="NO_OF_BAGS" class="form-control form-control-sm" value="${parsedData[i].NO_OF_BAGS || ''}"></td>
                    <td><input name="MUDGUN_HOLD_TIME" class="form-control form-control-sm" value="${parsedData[i].MUDGUN_HOLD_TIME || ''}"></td>

                    <td>
                        <select name="CLAY_LEAKAGE" class="form-select form-select-sm">
                            <option value=""></option>
                            <option value="YES" ${parsedData[i].CLAY_LEAKAGE === "YES" ? "selected" : ""}>YES</option>
                            <option value="NO" ${parsedData[i].CLAY_LEAKAGE === "NO" ? "selected" : ""}>NO</option>
                        </select>
                    </td>

                    <td>
                        <select name="BACK_FIRE" class="form-select form-select-sm">
                            <option value=""></option>
                            <option value="YES" ${parsedData[i].BACK_FIRE === "YES" ? "selected" : ""}>YES</option>
                            <option value="NO" ${parsedData[i].BACK_FIRE === "NO" ? "selected" : ""}>NO</option>
                        </select>
                    </td>
                </tr>`;
            }

            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
}