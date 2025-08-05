function Display_Mudgun_Details(lsSelectedFDate,IsSelectedFur) {                
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {
                        var parsedData = JSON.parse(result_Mudgun_Details);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {                            
                            tableBody += "<tr>";
                            tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                            tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].CLOSURE_MODE}'/></td>`;
                            tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].CLAY_QUANTITY}'/></td>`;                            
                            tableBody += `<td>
                                                <select class='form-select form-select-lg'>
                                                <option ${!parsedData[i].MG_CLAY_USED ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'LRH' ? 'selected': ''}>LRH</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'UBQ' ? 'selected': ''}>UBQ</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'SARVESH' ? 'selected': ''}>SARVESH</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'CALDYRS' ? 'selected': ''}>CALDYRS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(S)' ? 'selected': ''}>HARIMA(S) </option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)' ? 'selected': ''}>HARIMA(D) </option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'CORUS' ? 'selected': ''}>CORUS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'TRB' ? 'selected': ''}>TRB</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'VISUVIUS' ? 'selected': ''}>VISUVIUS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA-TWH4' ? 'selected': ''}>HARIMA-TWH4</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA-CPH4' ? 'selected': ''}>HARIMA-CPH4</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5' ? 'selected': ''}>HARIMA(D)-TWH5</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5K' ? 'selected': ''}>HARIMA(D)-TWH5K</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                </select>
                                              </td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].MUDGUN_NOZZLE}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input class='form-control form-control-lg' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                                                tableBody += `<td>
                                                <select class='form-select form-select-lg'>
                                                <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected': ''}>YES</option>
                                                <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected': ''}>NO</option>                                                
                                                </select>
                                              </td>`;                            
                            tableBody += `<td>
                                                <select class='form-select form-select-lg'>
                                                <option ${!parsedData[i].BACK_FIRE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected': ''}>YES</option>
                                                <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected': ''}>NO</option>
                                                </select>
                                              </td>`;
                            tableBody += "</tr>";
                        }
                        $("#Mudgun_Details").html(tableBody);
                    },
                });
            }
