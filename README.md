tableBody += `<td><select class='form-select form-select-md'>
                                <option ${parsedData[i].CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option>
                                <option ${parsedData[i].CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
                              </select></td>`;
