//=====================================================
// YOUR DISPLAY FUNCTION – MODIFIED
//=====================================================
function Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Carbon_Paste_Inj", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },

        success: function (result_Carbon_Paste_Inj) {

            var parsedData = JSON.parse(result_Carbon_Paste_Inj);
            var tableBody = "";

            //==========================================
            // NO DATA FOUND → BLANK ROW
            //==========================================
            if (!parsedData || parsedData.length == 0) {

                let autoShift = getShiftFromTime(lsSelectedFDate);

                tableBody += "<tr>";

                tableBody += `<td>
                    <input name="DATE_TIME"
                           class='form-control form-control-sm dt'
                           value='${lsSelectedFDate || ""}'/>
                </td>`;

                tableBody += `
                <td>
                    <select name="SHIFT"
                            class="form-control form-control-sm">

                        <option value="">Select</option>
                        <option value="A" ${autoShift=="A"?"selected":""}>A</option>
                        <option value="B" ${autoShift=="B"?"selected":""}>B</option>
                        <option value="C" ${autoShift=="C"?"selected":""}>C</option>

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


            //==========================================
            // DATA FOUND
            //==========================================
            for (var i = 0; i < parsedData.length; i++) {

                let finalDate = lsSelectedFDate ||
                                parsedData[i].DATE_TIME;

                let autoShift = getShiftFromTime(finalDate);

                let shift =
                    parsedData[i].SHIFT || autoShift;

                tableBody += "<tr>";

                tableBody += `<td>
                    <input name="DATE_TIME"
                           class='form-control form-control-sm dt'
                           value='${finalDate}'/>
                </td>`;

                tableBody += `
                <td>
                    <select name="SHIFT"
                            class="form-control form-control-sm">

                        <option value="">Select</option>

                        <option value="A" ${shift=="A"?"selected":""}>A</option>
                        <option value="B" ${shift=="B"?"selected":""}>B</option>
                        <option value="C" ${shift=="C"?"selected":""}>C</option>

                    </select>
                </td>`;

                tableBody += `<td>
                    <input name="BELOW_TUYERE"
                           class='form-control form-control-sm'
                           value='${parsedData[i].BELOW_TUYERE || ""}'/>
                </td>`;

                tableBody += `<td>
                    <input name="NO_OF_DRUM"
                           class='form-control form-control-sm'
                           value='${parsedData[i].NO_OF_DRUM || ""}'/>
                </td>`;

                tableBody += "</tr>";
            }

            $("#carbon_paste_inj tbody").html(tableBody);
        }
    });
}