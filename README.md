 $(document).on("click", "#TAP_Hot_Metal_Details tr", function () {
                debugger;
                // Always read data attribute as string
                let castNo = $(this).attr("data-castno");

                if (!castNo) return;
                castNo = castNo.trim();

                // Remove old highlights                
                $("#TAP_Hot_Metal_Details tr").removeClass("highlight");
                // Highlight both tables where CAST NO matches
                $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");                
            });
             function Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '/CastHouse/Get_TAP_Hole_Metal_Details',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Tap_Hole_Metal) {
                        var parsedData = JSON.parse(result_Tap_Hole_Metal);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {
                            debugger;
                            tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
                            tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                            tableBody += `<td><input name="TROUGH_NO" class='form-control form-control-lg' value='${parsedData[i].TROUGH_NO}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_ST_TIME" class='form-control form-control-lg' value='${parsedData[i].CAST_ST_TIME}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_END_TIME" class='form-control form-control-lg' value='${parsedData[i].CAST_END_TIME}' readonly/></td>`;
                            tableBody += `<td><input name="GUTKO" class='form-control form-control-lg' value='${parsedData[i].GUTKO}' readonly/></td>`;
                            tableBody += `<td><input name="CAST_DURATION" class='form-control form-control-lg' value='${parsedData[i].CAST_DURATION}' readonly/></td>`;
                            tableBody += `<td><input name="SPEED" class='form-control form-control-lg' value='${parsedData[i].SPEED}' readonly/></td>`;
                            tableBody += `<td><input name="NO_TLC" class='form-control form-control-lg' value='${parsedData[i].NO_TLC}' readonly/></td>`;
                            tableBody += `<td><input name="NO_OT" class='form-control form-control-lg' value='${parsedData[i].NO_OT}' readonly/></td>`;
                            tableBody += `<td><input name="CH_READY_TIME" class='form-control form-control-lg' value='${parsedData[i].CH_READY_TIME}'/></td>`;
                            tableBody += `<td><input name="SPLACING_WETNESS_TIME" class='form-control form-control-lg' value='${parsedData[i].SPLACING_WETNESS_TIME}'/></td>`;
                            tableBody += `<td>
                                      <select name="CAST_TYPE" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].CAST_TYPE ? 'selected': ''}></option>
                                      <option value="DRY" ${parsedData[i].CAST_TYPE === 'DRY' ? 'selected': ''}>DRY</option>
                                      <option value="NOT DRY" ${parsedData[i].CAST_TYPE === 'NOT DRY' ? 'selected': ''}>NOT DRY</option>
                                       </select></td>`;
                           tableBody += `<td>
                                      <select name="CAST_CLAY_COND" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].CAST_CLAY_COND ? 'selected': ''}></option>
                                      <option value="WET" ${parsedData[i].CAST_CLAY_COND === 'WET' ? 'selected': ''}>WET</option>
                                      <option value="DRY" ${parsedData[i].CAST_CLAY_COND === 'DRY' ? 'selected': ''}>DRY</option>
                                      <option value="EXCESS WET" ${parsedData[i].CAST_CLAY_COND === 'EXCESS WET' ? 'selected': ''}>EXCESS WET</option>
                                      <option value="BLEEDING" ${parsedData[i].CAST_CLAY_COND === 'BLEEDING' ? 'selected': ''}>BLEEDING</option>
                                       </select></td>`;
                           tableBody += `<td>
                                      <select name="TAPHOLE_BEHAVIOUR" class ="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].TAPHOLE_BEHAVIOUR ? 'selected': ''}></option>
                                      <option value="WIDE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected': ''}>WIDE</option>
                                      <option value="NORMAL" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected': ''}>NORMAL</option>
                                      <option value="WIDE+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected': ''}>WIDE+COKE TROUBLE</option>
                                      <option value="NORMAL+COKE TROUBLE" ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected': ''}>NORMAL+COKE TROUBLE</option>
                                       </select></td>`;
                           tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control form-control-lg' value='${parsedData[i].HM_BEFORE_SLAG}' /></td>`;
                           tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control form-control-lg'value='${parsedData[i].HM_AFTER_SLAG}' /></td>`;
                           tableBody += `<td><input name="HM_TEMP" class='form-control form-control-lg' value='${parsedData[i].HM_TEMP}'/></td>`;
                           tableBody += `<td><input name="HM_WEIGHT" class='form-control form-control-lg' value='${parsedData[i].HM_WEIGHT}'/></td>`;
                           tableBody += "</tr>";
                        }
                        $("#TAP_Hot_Metal_Details tbody").html(tableBody);
                    }
                });
            }
             .highlight{
            background-color:yellow!important;
        }
