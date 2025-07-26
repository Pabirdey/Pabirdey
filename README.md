function Display_Tap_Hole_Details() {
    var date = '2025-07-26';           // Example value (you can replace with dynamic one)
    var Fur_name = 'Furnace-A';        // Example value (you can get from input/dropdown)

    $.ajax({
        url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
        type: 'GET',
        data: { date: date, Fur_name: Fur_name },
        success: function (result_Tap_Hole_Metal) {
            var tableBody = "";
            for (var i = 0; i < result_Tap_Hole_Metal.length; i++) {
                tableBody += "<tr>";
                tableBody += `<td><input class='form-control form-control-sm' value='${result_Tap_Hole_Metal[i].CAST_NO}' readonly/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${result_Tap_Hole_Metal[i].TROUGH_NO}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${result_Tap_Hole_Metal[i].CAST_ST_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${result_Tap_Hole_Metal[i].CAST_END_TIME}'/></td>`;
                tableBody += "</tr>";
            }
            $("#CastDetailsBody tbody").html(tableBody);
        },
        error: function () {
            alert("Failed to load data.");
        }
    });
}
