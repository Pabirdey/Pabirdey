  function checkClay() {

            let p1 = Number(P1.value) || 0;
            let p2 = Number(P2.value) || 0;
            let p3 = Number(P3.value) || 0;

            if (p1 + p2 + p3 !== 100) {
                alert("Percentage must be 100");
                return;
            }

            let result = "";
            if (MG_CLAY1.value) result += MG_CLAY1.value + "(" + p1 + "%)";
            if (MG_CLAY2.value) result += (result ? "+" : "") + MG_CLAY2.value + "(" + p2 + "%)";
            if (MG_CLAY3.value) result += (result ? "+" : "") + MG_CLAY3.value + "(" + p3 + "%)";

            let rowIndex = $("#hdnRowIndex").val();
            let row = document.querySelectorAll("#Mudgun_Details tbody tr")[rowIndex];
            row.querySelector(".mgClayInput").value = result;

            bootstrap.Modal.getInstance(
                document.getElementById("mgClayOtherModal")
            ).hide();
        }
  function showDropdown(btn) {
            $('.mgClayList').hide();
            $(btn).next('.mgClayList').show();
        }

        function selectClay(item, rowIndex) {

            let list = item.parentElement;
            let input = list.previousElementSibling;

            if (item.innerText === "OTHERS") {
                $("#hdnRowIndex").val(rowIndex);
                new bootstrap.Modal(document.getElementById("mgClayOtherModal")).show();
            } else {
                input.value = item.innerText;
            }

            list.style.display = "none";
        }
 <input type="hidden" id="hdnRowIndex">

    <!-- ================= MODAL ================= -->
    <div class="modal fade" id="mgClayOtherModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center">MG CLAY WEIGHTAGE</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <!-- Clay 1 -->
                    <div class="row mb-2">
                        <div class="col-6">
                            <select id="MG_CLAY1" class="form-select">
                                <option value="">Clay1</option>
                                <option>ACE</option>
                                <option>BRL</option>
                            </select>
                        </div>
                        <div class="col-6">
                            <select id="P1" class="form-select">
                                <option value="">%</option>
                                <option>50</option>
                                <option>100</option>
                            </select>
                        </div>
                    </div>
                    <!-- Clay 2 -->
                    <div class="row mb-2">
                        <div class="col-6">
                            <select id="MG_CLAY2" class="form-select">
                                <option value="">Clay2</option>
                                <option>ACE</option>
                                <option>BRL</option>
                            </select>
                        </div>
                        <div class="col-6">
                            <select id="P2" class="form-select">
                                <option value="">%</option>
                                <option>20</option>
                            </select>
                        </div>
                    </div>
                    <!-- Clay 3 -->
                    <div class="row mb-2">
                        <div class="col-6">
                            <select id="MG_CLAY3" class="form-select">
                                <option value="">Clay3</option>
                                <option>ACE</option>
                                <option>BRL</option>
                            </select>
                        </div>
                        <div class="col-6">
                            <select id="P3" class="form-select">
                                <option value="">%</option>
                                <option>30</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-success" onclick="checkClay()">Save</button>
                    <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>
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
                            tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;
                            tableBody += `<td class="freeze-col">${parsedData[i].CAST_NO}</td>`;
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
                                                    <div onclick="selectItem(this, ${i})">CALDYRS</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(S)</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(D)</div>
                                                    <div onclick="selectItem(this, ${i})">CORUS</div>
                                                    <div onclick="selectItem(this, ${i})">TRB</div>
                                                    <div onclick="selectItem(this, ${i})">VISUVIUS</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA-TWH4</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA-CPH4</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(D)-TWH5</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(D)-TWH5K</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(D)TWH-5T</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA RWH-3</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA RWH-4</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(S)RW5F</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA RWH-5</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA RWH-6</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA CB1</div>
                                                    <div onclick="selectItem(this, ${i})">RW5F</div>
                                                    <div onclick="selectItem(this, ${i})">RG15</div>
                                                    <div onclick="selectItem(this, ${i})">RG15K</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA(D)TWH-7</div>
                                                    <div onclick="selectItem(this, ${i})">HARIMA CB2</div>
                                                    <div onclick="selectItem(this, ${i})">TWH5(BELPAHAR) </div>
                                                    <div onclick="selectItem(this, ${i})">CB2(BELPAHAR) </div>
                                                    <div onclick="selectItem(this, ${i})">TWH 8(BELPAHAR) </div>
                                                    <div onclick="selectItem(this, ${i})">TWH 8 K 1(BELPAHAR) </div>
                                                    <div onclick="selectClay(this, ${i})">OTHERS</div>
                                                </div>
                                            </div>
                                          </td>`;

                            /* ******** LOT NO TEXTBOX + BUTTON HERE ******** */
                            tableBody += `<td class="d-flex gap-0"><input name="LOT_NO" style="width:120px;"  value='${parsedData[i].LOT_NO}' />
                                        <button type="button" class ="btn btn-primary btn-sm getLot" data-castno="${parsedData[i].LOT_NO}">::</button></td>`;
                            tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-sm' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                            tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-sm' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;
                            tableBody += `<td>
                                                <select name="MUDGUN_NOZZLE" class ='form-select form-control-sm'>
                                                        <option ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''} value=""></option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                                                </select>
                                        </td>`;
                            tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-sm' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                            tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-sm' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                            tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-sm' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                            tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-sm' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                            tableBody += `<td>
                                        <select name="CLAY_LEAKAGE" class ='form-select form-control-sm'>
                                    <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected' : ''} value=""></option>
                                    <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected' : ''}>YES</option>
                                    <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected' : ''}>NO</option>
                                </select>
                            </td>`;

                            tableBody += `<td>
                                <select name="BACK_FIRE" class ='form-select form-control-sm'>
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
