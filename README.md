function Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Carbon_Paste_Inj", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },

        success: function (result_Carbon_Paste_Inj) {

            var parsedData = JSON.parse(result_Carbon_Paste_Inj);
            var tableBody = "";

            //==========================================
            // NO DATA FOUND
            //==========================================
            if (!parsedData || parsedData.length == 0) {

                tableBody += "<tr>";

                tableBody += `<td>
                    <input name="DATE_TIME"
                           class='form-control form-control-sm dt'
                           value='${lsSelectedFDate}'/>
                </td>`;

                tableBody += `
                <td>
                    <select name="SHIFT" class="form-control form-control-sm">
                        <option value="">Select</option>
                        <option value="A">A</option>
                        <option value="B">B</option>
                        <option value="C">C</option>
                    </select>
                </td>`;

                tableBody += `<td>
                    <input name="BELOW_TUYERE"
                           class='form-control form-control-sm'/>
                </td>`;

                tableBody += `<td>
                    <input name="NO_OF_DRUM"
                           class='form-control form-control-sm'/>
                </td>`;

                tableBody += "</tr>";

                $("#carbon_paste_inj tbody").html(tableBody);
                return;
            }
