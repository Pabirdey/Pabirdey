tableBody += `<td>
                                                <select class='form-select form-select-lg'>
                                                <option ${!parsedData[i].BACK_FIRE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected': ''}>YES</option>
                                                <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected': ''}>NO</option>
                                                </select>
                                              </td>`;
