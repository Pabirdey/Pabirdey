function Display_Tap_Hole_Details() {
    debugger;
    let date = "26-JUL-2025";
    let Fur_name = "C";

    $.ajax({
        url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
        type: 'GET',
        data: { date: date, Fur_Name: Fur_name }, // Match C# param names
        success: function (result_Tap_Hole_Metal) {
            debugger;
            // Since server returns string, we need to parse it
            var parsedData = JSON.parse(result_Tap_Hole_Metal);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {
                tableBody += "<tr>";
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].TROUGH_NO}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_ST_TIME}'/></td>`;
                tableBody += `<td><input class='form-control form-control-sm' value='${parsedData[i].CAST_END_TIME}'/></td>`;
                tableBody += "</tr>";
            }

            $("#TAP_Hot_Metal_Details tbody").html(tableBody);
        },
        error: function () {
            alert("Failed to load data.");
        }
    });
}

public JsonResult Get_TAP_Hole_Metal_Details(string date, string Fur_Name)
{
    string sql = string.Empty;
    DataTable dt = new DataTable();

    // Fixed: Use += to append the second SELECT for UNION
    sql = "SELECT CAST_NO,TROUGH_NO,CAST_ST_TIME,CAST_END_TIME,GUTKO,CAST_DURATION,SPEED,NO_TLC,NO_OT," +
          "CH_READY_TIME,SPLACING_WETNESS_TIME,CAST_TYPE,CAST_CLAY_COND,TAPHOLE_BEHAVIOUR,HM_BEFORE_SLAG," +
          "HM_AFTER_SLAG,HM_TEMP,HM_WEIGHT FROM Demo.T_CAST_DETAILS WHERE DATE_TIME='" + date + "' AND FUR_NAME='" + Fur_Name + "'" +
          " UNION " +
          "SELECT CAST_NO,TROUGH_NO,CAST_ST_TIME,CAST_END_TIME,GUTKO,CAST_DURATION,SPEED,NO_TLC,NO_OT," +
          "CH_READY_TIME,SPLACING_WETNESS_TIME,CAST_TYPE,CAST_CLAY_COND,TAPHOLE_BEHAVIOUR,HM_BEFORE_SLAG," +
          "HM_AFTER_SLAG,HM_TEMP,HM_WEIGHT FROM Demo.T_CAST_DETAILS WHERE DATE_TIME='" + date + "' AND FUR_NAME='" + Fur_Name + "'";

    dt = DAL.GetRecords(sql);
    string result_Tap_Hole_Metal = JsonConvert.SerializeObject(dt, Formatting.None);

    // Return as raw string (will need JSON.parse on client side)
    return Json(result_Tap_Hole_Metal, JsonRequestBehavior.AllowGet);
}
