function escapeHtml(text) {
    return text ? $('<div/>').text(text).html() : '';
}

function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '/CastHouse/Get_TAP_Hole_Metal_Details',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Tap_Hole_Metal) {
            var parsedData = JSON.parse(result_Tap_Hole_Metal);
            var tableBody = "";

            parsedData.forEach(function (data) {
                tableBody += "<tr>";
                tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${escapeHtml(data.CAST_NO)}' readonly/></td>`;
                tableBody += `<td><input name="TROUGH_NO" class='form-control form-control-lg' value='${escapeHtml(data.TROUGH_NO)}' readonly/></td>`;
                tableBody += `<td><input name="CAST_ST_TIME" class='form-control form-control-lg' value='${escapeHtml(data.CAST_ST_TIME)}' readonly/></td>`;
                tableBody += `<td><input name="CAST_END_TIME" class='form-control form-control-lg' value='${escapeHtml(data.CAST_END_TIME)}' readonly/></td>`;
                tableBody += `<td><input name="GUTKO" class='form-control form-control-lg' value='${escapeHtml(data.GUTKO)}' readonly/></td>`;
                tableBody += `<td><input name="CAST_DURATION" class='form-control form-control-lg' value='${escapeHtml(data.CAST_DURATION)}' readonly/></td>`;
                tableBody += `<td><input name="SPEED" class='form-control form-control-lg' value='${escapeHtml(data.SPEED)}' readonly/></td>`;
                tableBody += `<td><input name="NO_TLC" class='form-control form-control-lg' value='${escapeHtml(data.NO_TLC)}' readonly/></td>`;
                tableBody += `<td><input name="NO_OT" class='form-control form-control-lg' value='${escapeHtml(data.NO_OT)}' readonly/></td>`;
                tableBody += `<td><input name="CH_READY_TIME" class='form-control form-control-lg' value='${escapeHtml(data.CH_READY_TIME)}' /></td>`;
                tableBody += `<td><input name="SPLACING_WETNESS_TIME" class='form-control form-control-lg' value='${escapeHtml(data.SPLACING_WETNESS_TIME)}' /></td>`;
                
                // CAST_TYPE dropdown
                tableBody += `<td>
                    <select name="CAST_TYPE" class="form-select form-select-lg">
                        <option value="" ${(data.CAST_TYPE || '').trim() === '' ? 'selected' : ''}></option>
                        <option value="DRY" ${(data.CAST_TYPE || '').trim().toUpperCase() === 'DRY' ? 'selected' : ''}>DRY</option>
                        <option value="NOT DRY" ${(data.CAST_TYPE || '').trim().toUpperCase() === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
                    </select>
                </td>`;

                // CAST_CLAY_COND dropdown
                tableBody += `<td>
                    <select name="CAST_CLAY_COND" class="form-select form-select-lg">
                        <option value="" ${(data.CAST_CLAY_COND || '').trim() === '' ? 'selected' : ''}></option>
                        <option value="WET" ${(data.CAST_CLAY_COND || '').trim().toUpperCase() === 'WET' ? 'selected' : ''}>WET</option>
                        <option value="DRY" ${(data.CAST_CLAY_COND || '').trim().toUpperCase() === 'DRY' ? 'selected' : ''}>DRY</option>
                        <option value="EXCESS WET" ${(data.CAST_CLAY_COND || '').trim().toUpperCase() === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
                        <option value="BLEEDING" ${(data.CAST_CLAY_COND || '').trim().toUpperCase() === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
                    </select>
                </td>`;

                // TAPHOLE_BEHAVIOUR dropdown
                tableBody += `<td>
                    <select name="TAPHOLE_BEHAVIOUR" class="form-select form-select-lg">
                        <option value="" ${(data.TAPHOLE_BEHAVIOUR || '').trim() === '' ? 'selected' : ''}></option>
                        <option value="WIDE" ${(data.TAPHOLE_BEHAVIOUR || '').trim().toUpperCase() === 'WIDE' ? 'selected' : ''}>WIDE</option>
                        <option value="NORMAL" ${(data.TAPHOLE_BEHAVIOUR || '').trim().toUpperCase() === 'NORMAL' ? 'selected' : ''}>NORMAL</option>
                        <option value="WIDE+COKE TROUBLE" ${(data.TAPHOLE_BEHAVIOUR || '').trim().toUpperCase() === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option>
                        <option value="NORMAL+COKE TROUBLE" ${(data.TAPHOLE_BEHAVIOUR || '').trim().toUpperCase() === 'NORMAL+COKE TROUBLE' ? 'selected' : ''}>NORMAL+COKE TROUBLE</option>
                    </select>
                </td>`;

                tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control form-control-lg' value='${escapeHtml(data.HM_BEFORE_SLAG)}' /></td>`;
                tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control form-control-lg' value='${escapeHtml(data.HM_AFTER_SLAG)}' /></td>`;
                tableBody += `<td><input name="HM_TEMP" class='form-control form-control-lg' value='${escapeHtml(data.HM_TEMP)}' /></td>`;
                tableBody += `<td><input name="HM_WEIGHT" class='form-control form-control-lg' value='${escapeHtml(data.HM_WEIGHT)}' readonly/></td>`;
                tableBody += "</tr>";
            });

            $("#TAP_Hot_Metal_Details tbody").html(tableBody);
        }
    });
}
