function Display_Mudgun_Details(date, furnace){
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
        type: 'GET',
        data: { Fdate: date, Fur: furnace },
        success: function(result){
            let parsedData = JSON.parse(result);
            let tableBody = "";
            for(let i=0;i<parsedData.length;i++){
                tableBody += "<tr>";
                tableBody += `<td>${parsedData[i].CAST_NO}</td>`;
                tableBody += `<td>
                                <select class="form-select form-select-sm">
                                    <option value="" ${parsedData[i].CLOSURE_MODE==""?'selected':''}></option>
                                    <option value="MUDGUN" ${parsedData[i].CLOSURE_MODE=="MUDGUN"?'selected':''}>MUDGUN</option>
                                    <option value="NULL" ${parsedData[i].CLOSURE_MODE=="NULL"?'selected':''}>NULL</option>
                                </select>
                              </td>`;
                tableBody += `<td><input class="form-control form-control-sm" value="${parsedData[i].CLAY_QUANTITY}"></td>`;
                // Editable MG Clay input + dropdown + modal
                tableBody += `<td>
                                <div class="mgClayWrapper">
                                    <input type="text" class ="form-control form-control-sm mgClayInput" value="${parsedData[i].MG_CLAY_USED}">
                                    <button type="button" class="btn btn-sm btn-secondary" onclick="showDropdown(this)">▼</button>
                                    <div class="mgClayList">
                                        <div onclick="selectClay(this, ${i})">ACE</div>
                                        <div onclick="selectClay(this, ${i})">BRL</div>
                                        <div onclick="selectClay(this, ${i})">LRH</div>
                                        <div onclick="selectClay(this, ${i})">UBQ</div>
                                        <div onclick="selectClay(this, ${i})">OTHERS</div>
                                    </div>
                                </div>
                              </td>`;

                tableBody += `<td>${parsedData[i].LOT_NO}</td>`;
                tableBody += `<td>${parsedData[i].NO_OF_BAGS}</td>`;
                tableBody += "</tr>";
            }
            $('#Mudgun_Details tbody').html(tableBody);
        }
    });
}
