 tableBody += "<td><select class='form-select form-select-md'>";
                            tableBody += `<option value=""></option>`;
                            tableBody += `<option ${(data.CAST_CLAY_COND === 'WET') ? 'selected' : ''}>WET</option>`;
                            tableBody += `<option ${(data.CAST_CLAY_COND === 'DRY') ? 'selected' : ''}>DRY</option>`;
                            tableBody += `<option ${(data.CAST_CLAY_COND === 'EXCESS WET') ? 'selected' : ''}>EXCESS WET</option>`;
                            tableBody += `<option ${(data.CAST_CLAY_COND === 'BLEEDING') ? 'selected' : ''}>BLEEDING</option>`;
                            tableBody += "</select></td>";
