function Display_Tap_Hole_Details() {    
                             let date = "26-JUL-2025";
                             let Fur_name = "C";
                    $.ajax({
                            url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
                            type: 'GET',
                            data: { date: date, Fur_Name: Fur_name }, 
                            success: function (result_Tap_Hole_Metal) {          
                            var parsedData = JSON.parse(result_Tap_Hole_Metal);
                            var tableBody = "";
                            for (var i = 0; i < parsedData.length; i++) {
                                tableBody += "<tr>";
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].CAST_NO}' readonly/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].TROUGH_NO}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].CAST_ST_TIME}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].CAST_END_TIME}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].GUTKO}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].CAST_DURATION}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].SPEED}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].NO_TLC}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].NO_OT}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].CH_READY_TIME}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].SPLACING_WETNESS_TIME}'/></td>`;
                                tableBody += `<td><select class='form-select form-select-md'><option ${data[i].CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option><option ${data[i].CAST_TYPE === 'NOT DRY' ? 'selected': ''}>NOT DRY</option></select></td>`;                                
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].NO_TLC}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].NO_TLC}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].HM_BEFORE_SLAG}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].HM_AFTER_SLAG}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].HM_TEMP}'/></td>`;
                                tableBody += `<td><input class='form-control form-control-md' value='${parsedData[i].HM_WEIGHT}'/></td>`;
                                tableBody += "</tr>";
                                }
                            $("#TAP_Hot_Metal_Details").html(tableBody);
                         },                                
                     });
             }
     });
