function SaveCastHouseData() {
            debugger;
            var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr");
            var CastHouseData = [];
            rows.forEach(function(row) {
                var rowData = {};
                var inputs = row.querySelectorAll("input, select");
                inputs.forEach(function(input) {
                    rowData[input.name] = input.value;
                });

                CastHouseData.push(rowData);
                console.log(CastHouseData);
            });            
            //var selectedDate = document.getElementById("selectedDate").value;
            //var selectedFurnace = document.getElementById("selectedFurnace").value;           
            $.ajax({
                url: '/CastHouse/SaveCastHouseData',
                type: 'POST',
                contentType: 'application/json',
                data: JSON.stringify(CastHouseData),
                success: function (res) {
                    alert("Saved successfully!");
                },
                error: function () {
                    alert("Save failed.");
                }
            });
        }

        function Display_Tap_Hole_Details(lsSelectedFDate,IsSelectedFur) {                            
                    $.ajax({
                            url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
                            type: 'GET',
                            data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                            success: function (result_Tap_Hole_Metal) {
                             var parsedData = JSON.parse(result_Tap_Hole_Metal);
                            var tableBody = "";
                            for (var i = 0; i < parsedData.length; i++) {                                
                                tableBody += "<tr>";
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
                                tableBody += `<td><select name="CAST_TYPE" class='form-select form-select-lg'><option ${parsedData[i].CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option><option ${parsedData[i].CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option></select></td>`;
                                tableBody += `<td>
                                                <select name="CAST_CLAY_COND" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].CAST_CLAY_COND ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].CAST_CLAY_COND === 'WET' ? 'selected' : ''}>WET</option>
                                                <option ${parsedData[i].CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
                                                <option ${parsedData[i].CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
                                                <option ${parsedData[i].CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
                                                </select>
                                              </td>`;
                                tableBody += `<td><select name="TAPHOLE_BEHAVIOUR" class='form-select form-select-lg'><option ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected' : ''}>WIDE</option><option ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected' : ''}>NORMAL</option><option ${parsedData[i].TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option><option ${parsedData[i].TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected' : 'NORMAL+COKE TROUBLE'}></option></select></td>`;
                                tableBody += `<td><input name="HM_BEFORE_SLAG" class='form-control form-control-lg' value='${parsedData[i].HM_BEFORE_SLAG}'/></td>`;
                                tableBody += `<td><input name="HM_AFTER_SLAG" class='form-control form-control-lg' value='${parsedData[i].HM_AFTER_SLAG}'/></td>`;
                                tableBody += `<td><input name="HM_TEMP" class='form-control form-control-lg' value='${parsedData[i].HM_TEMP}'/></td>`;
                                tableBody += `<td><input name="HM_WEIGHT" class='form-control form-control-lg' value='${parsedData[i].HM_WEIGHT}' readonly/></td>`;
                                tableBody += "</tr>";
                                }
                            $("#TAP_Hot_Metal_Details").html(tableBody);
                         },
                     });
            }
