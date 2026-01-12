<script>
function toggleList(index) {
    var list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

function selectItem(el, index) {
    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    // OPTIONAL: if OTHERS clicked
    if (el.innerText === "OTHERS") {
        // open modal / show textbox / anything
        console.log("OTHERS selected at row:", index);
    }
}

// Close all lists when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {

        document.querySelectorAll(".list-box").forEach(function (l) {
            l.style.display = "none";
        });
    }
});
</script>

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

                            tableBody += `
                                        <td>
                                        <div class="input-wrapper">
                                        <input type="text" class="form-control form-control-lg clay-input" id="clayInput_${i}" name="MG_CLAY_USED" value="${parsedData[i].MG_CLAY_USED || ''}">
                                        <div class ="arrow-btn" onclick="toggleList(${i})">▼</div>
                                        </div>
                                        <div class="list-box" id="list_${i}">
                                        <div onclick="selectItem(this, ${i})">ACE</div>
                                        <div onclick="selectItem(this, ${i})">BRL</div>
                                        <div onclick="selectItem(this, ${i})">LRH</div>
                                        <div onclick="selectItem(this, ${i})">UBQ</div>
                                        <div onclick="selectItem(this, ${i})">OTHERS</div>
                                        <div onclick="selectItem(this, ${i})">SARVESH</div>
                                        <div onclick="selectItem(this, ${i})">CALDYRS</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(S)</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(D) </div>
                                        <div onclick="selectItem(this, ${i})">CORUS </div>
                                        <div onclick="selectItem(this, ${i})">TRB</div>
                                        <div onclick="selectItem(this, ${i})">VISUVIUS</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA-TWH4</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA-CPH4</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(D)-TWH5</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(D)-TWH5K</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(D)TWH-5T</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA RWH-3</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA RWH-4</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(S) RW5F</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA RWH-5</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA RWH-6</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA CB 1</div>
                                        <div onclick="selectItem(this, ${i})">RW5F</div>
                                        <div onclick="selectItem(this, ${i})">RG15</div>
                                        <div onclick="selectItem(this, ${i})">RG15K</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA(D) TWH-7</div>
                                        <div onclick="selectItem(this, ${i})">HARIMA CB 2</div>
                                        <div onclick="selectItem(this, ${i})">TWH5(BELPAHAR)</div>
                                        <div onclick="selectItem(this, ${i})">CB2(BELPAHAR)</div>
                                        <div onclick="selectItem(this, ${i})">TWH 8(BELPAHAR)</div>
                                        <div onclick="selectItem(this, ${i})">TWH 8 K 1(BELPAHAR)</div>
                                </div>
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
             <div class="modal fade" id="clayModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">

                <!-- HEADER -->
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>

                <!-- BODY -->
                <div class="modal-body">
                    <div class="title-box">Weightage of Clay</div>
                    <div class="clay-box">
                        <!-- Clay 1 (DROPDOWN) -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay1</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="clay1">
                                    <option value="">-- Select Clay1 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                        <!-- Clay 2 -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay2</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay2"> -->
                                <select class="form-select clay-input" id="clay2">
                                    <option value="">-- Select Clay2 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                        <!-- Clay 3 -->
                        <div class="row align-items-center">
                            <div class="col-2 clay-label">Clay3</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay3"> -->
                                <select class="form-select clay-input" id="clay3">
                                    <option value="">-- Select Clay3 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                    </div>

                </div>

                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-save" onclick="saveData()">Save</button>
                    <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>
