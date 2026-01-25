
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
                                    <input type="text" class="form-control form-control-sm mgClayInput" value="${parsedData[i].MG_CLAY}">
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

// Show dropdown
function showDropdown(btn){
    var lists = document.querySelectorAll('.mgClayList');
    for(var i=0;i<lists.length;i++){ lists[i].style.display='none'; }
    var list = btn.nextElementSibling;
    list.style.display = 'block';
    document.addEventListener('click', function handler(e){
        if(!list.contains(e.target) && e.target !== btn){
            list.style.display = 'none';
            document.removeEventListener('click', handler);
        }
    });
}

// Select item from dropdown
function selectClay(item, rowIndex){
    var list = item.parentElement;
    var input = list.previousElementSibling;
    if(item.innerText === "OTHERS"){
        $("#hdnRowIndex").val(rowIndex);
        $("#txtOtherMGClay").val(input.value); // show current value
        let modalEl = document.getElementById("mgClayOtherModal");
        let modal = new bootstrap.Modal(modalEl);
        modal.show();
    } else {
        input.value = item.innerText;
    }
    list.style.display = 'none';
}
[HttpGet]
        public JsonResult Get_Display_Mudgun_Details(string Fdate, string Fur)
        {
            DataTable dt_Mudgun_Details = new DataTable();
            string sql = string.Empty;
            sql = "SELECT Decode(CAST_NO,NULL,' ',CAST_NO) CAST_NO, Decode(CLOSURE_MODE,NULL,' ',CLOSURE_MODE) CLOSURE_MODE,";
            sql += "Decode(CLAY_QUANTITY,NULL,' ',CLAY_QUANTITY) CLAY_QUANTITY, Decode(MG_CLAY_USED,NULL,' ',MG_CLAY_USED) MG_CLAY_USED,";
            sql += "Decode(LOT_NO,NULL,' ',LOT_NO) LOT_NO, Decode(NO_OF_BAGS,NULL,' ',NO_OF_BAGS) NO_OF_BAGS,";
            sql += "Decode(MUDGUN_HOLD_TIME,NULL,' ',MUDGUN_HOLD_TIME) MUDGUN_HOLD_TIME, Decode(MUDGUN_NOZZLE,NULL,' ',MUDGUN_NOZZLE) MUDGUN_NOZZLE,";
            sql += "Decode(MNOZZLE_BEF_CLOSING,NULL,' ',MNOZZLE_BEF_CLOSING) MNOZZLE_BEF_CLOSING, Decode(MNOZZLE_AFT_CLOSING,NULL,' ',MNOZZLE_AFT_CLOSING) MNOZZLE_AFT_CLOSING,";
            sql += "Decode(INIT_PLUGIN_PRESSURE,NULL,' ',INIT_PLUGIN_PRESSURE) INIT_PLUGIN_PRESSURE, Decode(MAX_PLUGIN_PRESSURE,NULL,' ',MAX_PLUGIN_PRESSURE) MAX_PLUGIN_PRESSURE,";
            sql += "Decode(FINAL_PLUGIN_PRESSURE,NULL,' ',FINAL_PLUGIN_PRESSURE) FINAL_PLUGIN_PRESSURE, Decode(PRESS_ON_FORCE,NULL,' ',PRESS_ON_FORCE) PRESS_ON_FORCE,";
            sql += "Decode(CLAY_LEAKAGE,NULL,' ',CLAY_LEAKAGE) CLAY_LEAKAGE, Decode(BACK_FIRE,NULL,' ',BACK_FIRE) BACK_FIRE FROM ";
            sql += "Test.T_CAST_DETAILS WHERE DATE_TIME = TO_DATE('" + Fdate + "', 'DD-MM-YYYY') AND FUR_NAME = '" + Fur + "' ";
            sql += "UNION ";
            sql += "SELECT Decode(CAST_NO,NULL,' ',CAST_NO) CAST_NO, Decode(CLOSURE_MODE,NULL,' ',CLOSURE_MODE) CLOSURE_MODE,";
            sql += "Decode(CLAY_QUANTITY,NULL,' ',CLAY_QUANTITY) CLAY_QUANTITY, Decode(MG_CLAY_USED,NULL,' ',MG_CLAY_USED) MG_CLAY_USED,";
            sql += "Decode(LOT_NO,NULL,' ',LOT_NO) LOT_NO, Decode(NO_OF_BAGS,NULL,' ',NO_OF_BAGS) NO_OF_BAGS,";
            sql += "Decode(MUDGUN_HOLD_TIME,NULL,' ',MUDGUN_HOLD_TIME) MUDGUN_HOLD_TIME, Decode(MUDGUN_NOZZLE,NULL,' ',MUDGUN_NOZZLE) MUDGUN_NOZZLE,";
            sql += "Decode(MNOZZLE_BEF_CLOSING,NULL,' ',MNOZZLE_BEF_CLOSING) MNOZZLE_BEF_CLOSING, Decode(MNOZZLE_AFT_CLOSING,NULL,' ',MNOZZLE_AFT_CLOSING) MNOZZLE_AFT_CLOSING,";
            sql += "Decode(INIT_PLUGIN_PRESSURE,NULL,' ',INIT_PLUGIN_PRESSURE) INIT_PLUGIN_PRESSURE, Decode(MAX_PLUGIN_PRESSURE,NULL,' ',MAX_PLUGIN_PRESSURE) MAX_PLUGIN_PRESSURE,";
            sql += "Decode(FINAL_PLUGIN_PRESSURE,NULL,' ',FINAL_PLUGIN_PRESSURE) FINAL_PLUGIN_PRESSURE, Decode(PRESS_ON_FORCE,NULL,' ',PRESS_ON_FORCE) PRESS_ON_FORCE,";
            sql += "Decode(CLAY_LEAKAGE,NULL,' ',CLAY_LEAKAGE) CLAY_LEAKAGE, Decode(BACK_FIRE,NULL,' ',BACK_FIRE) BACK_FIRE FROM ";
            sql += "Test.T_CAST_DETAILS WHERE DATE_TIME = TO_DATE('" + Fdate + "', 'DD-MM-YYYY') AND FUR_NAME = '" + Fur + "'";
            dt_Mudgun_Details = DAL.GetRecords(sql);
            string result_Mudgun_Details = JsonConvert.SerializeObject(dt_Mudgun_Details, Formatting.None);
            return Json(result_Mudgun_Details, JsonRequestBehavior.AllowGet);
        }

