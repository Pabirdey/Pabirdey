 function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {

                        var parsedData = JSON.parse(result_Mudgun_Details);
                        var tableBody = "";

                        for (var i = 0; i < parsedData.length; i++) {

                            tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;

                            tableBody += `<td>
                                <input name="CAST_NO"
                                       class='form-control form-control-lg'
                                       value='${parsedData[i].CAST_NO}' readonly/>
                              </td>`;

                            tableBody += `<td>
                    <select name="CLOSURE_MODE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].CLOSURE_MODE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>`;

                            tableBody += `<td>
                                <input name="CLAY_QUANTITY" class ='form-control form-control-lg' value='${parsedData[i].CLAY_QUANTITY}'/>
                                </td>`;
                            tableBody += `<td>
                                    <input name="MG_CLAY_USED" list="clayOptions_${i}" class ="form-control form-control-lg" value="${parsedData[i].MG_CLAY_USED || ''}">
                                    <datalist id="clayOptions_${i}">
                                    ${[
                                        'ACE', 'BRL', 'LRH', 'UBQ', 'SARVESH', 'CALDYRS', 'HARIMA(S)', 'HARIMA(D)', 'CORUS',
                                        'TRB', 'VISUVIUS', 'HARIMA-TWH4', 'HARIMA-CPH4', 'HARIMA(D)-TWH5', 'HARIMA(D)-TWH5K',
                                        'HARIMA(D)-TWH-5T', 'HARIMA RWH-3', 'HARIMA RWH-4', 'HARIMA(S)RW5F', 'HARIMA(S)RG15K',
                                        'HARIMA RWH-5', 'HARIMA RWH-6', 'HARIMA CB 1', 'RW5F', 'RG15', 'RG15K', 'HARIMA(D)TWH-7',
                                        'HARIMA CB 2', 'TWH5(BELPAHAR)', 'CB2(BELPAHAR)', 'TWH 8(BELPAHAR)', 'TWH 8 K 1(BELPAHAR)',
                                        'OTHERS'
                                    ].map(option => `<option value="${option}">${option}</option>`).join("")}
                                </datalist>
                            </td>`;
                            /* ******** LOT NO TEXTBOX + BUTTON HERE ******** */
                            tableBody += `<td class="d-flex gap-0"><input name="LOT_NO" style="width:120px;"  value='${parsedData[i].LOT_NO}' />
                            <button type="button" class ="btn btn-primary btn-sm getLot" data-castno="${parsedData[i].LOT_NO}">::</button></td>`;
                            tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-lg' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                            tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-lg' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;
                            tableBody += `<td>
                                    <select name="MUDGUN_NOZZLE" class='form-select form-select-lg'>
                                            <option ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''} value=""></option>
                                            <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                                            <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                                    </select>
                            </td>`;
                            tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                            tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                            tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-lg' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                            tableBody += `<td>
                    <select name="CLAY_LEAKAGE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                            tableBody += `<td>
                    <select name="BACK_FIRE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].BACK_FIRE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                        <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                    </select>
                </td>`;

                            tableBody += `</tr>`;
                        }

                        $("#Mudgun_Details tbody").html(tableBody);
                    }
                });
            }
