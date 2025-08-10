tableBody += `<td><select name="CAST_CLAY_COND" class='form-select form-select-md'>`;
tableBody += `<option value=""></option>`;
tableBody += `<option value="WET" ${(data.CAST_CLAY_COND === 'WET') ? 'selected' : ''}>WET</option>`;
tableBody += `<option value="DRY" ${(data.CAST_CLAY_COND === 'DRY') ? 'selected' : ''}>DRY</option>`;
tableBody += `<option value="EXCESS WET" ${(data.CAST_CLAY_COND === 'EXCESS WET') ? 'selected' : ''}>EXCESS WET</option>`;
tableBody += `<option value="BLEEDING" ${(data.CAST_CLAY_COND === 'BLEEDING') ? 'selected' : ''}>BLEEDING</option>`;
tableBody += `</select></td>`;
