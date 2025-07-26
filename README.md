  <div class="table-responsive scrollable-table">
                        <table class="table table-bordered table-sm text-center align-middle">
                            <thead class="table-light">
                                <tr>
                                    <th>Cast No</th>
                                    <th>Trough No</th>
                                    <th>Cast Start</th>
                                    <th>Cast End</th>
                                    <th>Gutko</th>
                                    <th>Cast Duration</th>
                                    <th>Casting Rate(t/min)</th>
                                    <th>TLC</th>
                                    <th>OT</th>
                                    <th>Cast Ready Time</th>
                                    <th>Splashing/Wetness Time</th>
                                    <th>Cast Type</th>
                                    <th>Clay Condition</th>
                                    <th>Taphole Behaviour at End Cast</th>
                                    <th class="Long_Heading">HMT Before Slag</th>
                                    <th class="Long_Heading">HMT After Slag</th>
                                    <th class="Long_Heading">Final HM Temp</th>
                                    <th class="Long_Heading">HM Weight</th>
                                </tr>
                            </thead>
                            <tbody id="TAP_Hot_Metal_Details"></tbody>
                        </table>
                    </div>

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
                tableBody += `<td><input class='form-control+ form-control-sm' value='${parsedData[i].CAST_END_TIME}'/></td>`;
                tableBody += "</tr>";
            }

            $("#TAP_Hot_Metal_Details tbody").html(tableBody);
        },
        error: function () {
            alert("Failed to load data.");
        }
    });
}
