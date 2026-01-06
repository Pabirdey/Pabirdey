function Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Carbon_Paste_Inj", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Carbon_Paste_Inj) {

            var parsedData = JSON.parse(result_Carbon_Paste_Inj);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                let shift = parsedData[i].SHIFT || "";

                tableBody += "<tr>";
                tableBody += `<td><input name="DATE_TIME" class='form-control form-control-sm' value='${parsedData[i].DATE_TIME}'/></td>`;

                // SHIFT DROPDOWN
                tableBody += `
                    <td>
                        <select name="SHIFT" class="form-control form-control-sm">
                            <option value="">Select</option>
                            <option value="A" ${shift === "A" ? "selected" : ""}>A</option>
                            <option value="B" ${shift === "B" ? "selected" : ""}>B</option>
                            <option value="C" ${shift === "C" ? "selected" : ""}>C</option>
                        </select>
                    </td>
                `;

                tableBody += `<td><input name="BELOW_TUYERE" class='form-control form-control-sm' value='${parsedData[i].BELOW_TUYERE}'/></td>`;
                tableBody += `<td><input name="NO_OF_DRUM" class='form-control form-control-sm' value='${parsedData[i].NO_OF_DRUM}'/></td>`;
                tableBody += "</tr>";
            }

            $("#carbon_paste_inj tbody").html(tableBody);
        },
    });
}