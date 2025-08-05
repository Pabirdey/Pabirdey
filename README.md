function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '/CastHouse/Get_TAP_Hole_Metal_Details', // FIXED: plain string URL
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Tap_Hole_Metal) {
            var parsedData = JSON.parse(result_Tap_Hole_Metal);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {
                var data = parsedData[i];
                tableBody += "<tr>";
                tableBody += `<td><input name="CAST_NO" class='form-control' value='${data.CAST_NO || ''}' readonly/></td>`;
                tableBody += `<td><input name="TROUGH_NO" class='form-control' value='${data.TROUGH_NO || ''}' readonly/></td>`;
                tableBody += `<td><input name="CAST_ST_TIME" class='form-control' value='${data.CAST_ST_TIME || ''}' readonly/></td>`;
                tableBody += `<td><input name="CAST_END_TIME" class='form-control' value='${data.CAST_END_TIME || ''}' readonly/></td>`;
                tableBody += `<td><input name="GUTKO" class='form-control' value='${data.GUTKO || ''}' readonly/></td>`;
                tableBody += `<td><input name="CAST_DURATION" class='form-control' value='${data.CAST_DURATION || ''}' readonly/></td>`;
                tableBody += `<td><input name="SPEED" class='form-control' value='${data.SPEED || ''}' readonly/></td>`;
                tableBody += `<td><input name="NO_TLC" class='form-control' value='${data.NO_TLC || ''}' readonly/></td>`;
                tableBody += `<td><input name="NO_OT" class='form-control' value='${data.NO_OT || ''}' readonly/></td>`;
                tableBody += `<td><input name="CH_READY_TIME" class='form-control' value='${data.CH_READY_TIME || ''}' /></td>`;
                tableBody += `<td><input name="SPLACING_WETNESS_TIME" class='form-control' value='${data.SPLACING_WETNESS_TIME || ''}' /></td>`;
                tableBody += `<td><select name="CAST_TYPE" class='form-select'>
                                <option ${data.CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option>
                                <option ${data.CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
                              </select></td>`;
                tableBody += `<td><select name="CAST_CLAY_COND" class='form-select'>
                                <option value="" ${!data.CAST_CLAY_COND ? 'selected' : ''}></option>
                                <option ${data.CAST_CLAY_COND === 'WET' ? 'selected' : ''}>WET</option>
                                <option ${data.CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
                                <option ${data.CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
                                <option ${data.CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
                              </select></td>`;
                tableBody += `<td><select name="TAPHOLE_BEHAVIOUR" class='form-select'>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected' : ''}>WIDE</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected' : ''}>NORMAL</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option>
                                <option ${data.TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected' : ''}>NORMAL+COKE TROUBLE</option>
                              </select></td>`;
                tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control' value='${data.HM_BEFORE_SLAG || ''}' /></td>`;
                tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control' value='${data.HM_AFTER_SLAG || ''}' /></td>`;
                tableBody += `<td><input name="HM_TEMP" class='form-control' value='${data.HM_TEMP || ''}' /></td>`;
                tableBody += `<td><input name="HM_WEIGHT" class='form-control' value='${data.HM_WEIGHT || ''}' readonly/></td>`;
                tableBody += "</tr>";
            }

            // ✅ FIX: Target tbody only
            $("#TAP_Hot_Metal_Details tbody").html(tableBody);
        },
        error: function (err) {
            console.error("AJAX error:", err);
            alert("Failed to load data");
        }
    });
}
