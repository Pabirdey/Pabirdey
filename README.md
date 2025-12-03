var clayList = [];  // global list

function LoadClayMasterList() {
    return $.ajax({
        url: '@Url.Action("GetClayList", "CastHouse")',
        type: 'GET',
        success: function (data) {
            clayList = data;  // save list
        }
    });
}

function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {

    LoadClayMasterList().then(function () {

        $.ajax({
            url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
            type: 'GET',
            data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
            success: function (result_Mudgun_Details) {

                var parsedData = JSON.parse(result_Mudgun_Details);
                var tableBody = "";

                for (var i = 0; i < parsedData.length; i++) {

                    tableBody += "<tr>";
                    tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;

                    // 🔽 Dynamic Clay List from Oracle
                    let clayOptions = `<option value=""></option>`;
                    clayList.forEach(clay => {
                        clayOptions += `<option ${parsedData[i].MG_CLAY_USED === clay ? "selected" : ""}>${clay}</option>`;
                    });

                    tableBody += `<td>
                        <select name="MG_CLAY_USED" class='form-select form-select-lg'>
                            ${clayOptions}
                        </select>
                    </td>`;

                    // Continue your remaining fields below 👇
                    tableBody += `<td><input name="LOT_NO" class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/></td>`;
                    tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-lg' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                    tableBody += "</tr>";
                }

                $("#Mudgun_Details tbody").html(tableBody);
            }
        });
    });
}