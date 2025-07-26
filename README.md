function Display_Tap_Hole_Details() {
    debugger;
    let date = "26-JUL-2025";
    let Fur_name = "C";

    $.ajax({
        url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
        type: 'GET',
        data: { date: date, Fur_Name: Fur_name },
        success: function (result_Tap_Hole_Metal) {
            debugger;
            var parsedData = JSON.parse(result_Tap_Hole_Metal);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {
                tableBody += "<tr>";
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].TROUGH_NO}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_ST_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_END_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].GUTKO}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_DURATION}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].SPEED}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].NO_TLC}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].NO_OT}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CH_READY_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].SPLACING_WETNESS_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_TYPE}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_CLAY_COND}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].TAPHOLE_BEHAVIOUR}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].HM_BEFORE_SLAG}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].HM_AFTER_SLAG}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].HM_TEMP}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].HM_WEIGHT}'/></td>`;
                tableBody += "</tr>";
            }

            // FIXED: Don't use `tbody` again in selector
            $("#TAP_Hot_Metal_Details").html(tableBody);
        },
        error: function () {
            alert("Failed to load data.");
        }
    });
}
