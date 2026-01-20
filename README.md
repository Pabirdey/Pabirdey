 function saveCarbonPaste() {
            debugger;
            var dataList = [];
            var rows = document.querySelectorAll("#carbon_paste_inj tbody tr");
            for (var i = 0; i < rows.length; i++) {
                var dt = rows[i].querySelector("#txtDate").value;
                var shift = rows[i].querySelector("#lstShift").value;
                var tuyere = rows[i].querySelector("#txtbelow_tuy").value;
                var drum = rows[i].querySelector("#txtNoofDrum").value;
                var obj = {
                    DATE_TIME: dt,
                    SHIFT: shift,
                    BELOW_TUYERE: tuyere,
                    NO_OF_DRUM: drum
                };

                dataList.push(obj);
            }            
            localStorage.setItem(
                "CARBON_PASTE_DATA",
                JSON.stringify(dataList)
            );
            alert("Saved Successfully!");
            loadCarbonPaste_JS();
        }
           <fieldset class="border rounded p-3 shadow-sm">
                            <legend class="float-none w-auto px-2">
                                Carbon Paste Inj
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">Save</button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:255px;">
                                <table class="table table-bordered table-sm text-center align-middle" id="carbon_paste_inj">
                                    <thead>
                                        <tr>
                                            <th class="Heading_Small" id="txtDate">Date Time</th>
                                            <th class="Heading_Small" id="lstShift">Shift</th>
                                            <th class="Heading_Small" id="txtbelow_tuy">Below Tuyere</th>
                                            <th class="Heading_Small" id="txtNoofDrum">No of Drum</th>
                                        </tr>
                                    </thead>
                                    <tbody></tbody>
                                </table>
                            </div>
                        </fieldset>
                        function Display_Carbon_Paste_Inj(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Carbon_Paste_Inj", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Carbon_Paste_Inj) {
                        var parsedData = JSON.parse(result_Carbon_Paste_Inj);
                        var tableBody = "";                        
                        if (!parsedData || parsedData.length == 0) {
                            let autoShift = getShiftFromTime(lsSelectedFDate);
                            tableBody += "<tr>";
                            tableBody += `<td><input name="DATE_TIME" class='form-control form-control-sm dt' value='${lsSelectedFDate || ""}'/></td>`;
                            tableBody += `<td>
                                <select name="SHIFT" class ="form-control form-control-sm">
                                    <option value="">Select</option>
                                    <option value="A" ${autoShift == "A" ? "selected" : ""}>A</option>
                                    <option value="B" ${autoShift == "B" ? "selected" : ""}>B</option>
                                    <option value="C" ${autoShift == "C" ? "selected" : ""}>C</option>
                              </select>
                           </td>`;
                            tableBody += `<td><input name="BELOW_TUYERE" class='form-control form-control-sm'/></td>`;
                            tableBody += `<td><input name="NO_OF_DRUM"   class='form-control form-control-sm'/></td>`;
                            tableBody += "</tr>";
                            $("#carbon_paste_inj tbody").html(tableBody);
                            return;
                        }                       
                        for (var i = 0; i < parsedData.length; i++) {
                            let finalDate = lsSelectedFDate ||parsedData[i].DATE_TIME;
                            let autoShift = getShiftFromTime(finalDate);
                            let shift =parsedData[i].SHIFT || autoShift;
                            tableBody += "<tr>";
                            tableBody += `<td><input name="DATE_TIME" class='form-control form-control-sm dt' value='${finalDate}'/></td>`;
                            tableBody += `<td><select name="SHIFT"    class="form-control form-control-sm">
                                <option value="">Select</option>
                                    <option value="A" ${shift == "A" ? "selected" : ""}>A</option>
                                    <option value="B" ${shift == "B" ? "selected": ""}>B</option>
                                    <option value="C" ${shift == "C" ? "selected": ""}>C</option>
                                </select>
                           </td>`;
                            tableBody += `<td><input name="BELOW_TUYERE" class='form-control form-control-sm' value='${parsedData[i].BELOW_TUYERE || ""}'/></td>`;
                            tableBody += `<td><input name="NO_OF_DRUM"   class='form-control form-control-sm' value='${parsedData[i].NO_OF_DRUM || ""}'/></td>`;
                            tableBody += "</tr>";
                        }
                        $("#carbon_paste_inj tbody").html(tableBody);
                    }
                });
            }
            function getShiftFromTime(dt) {
                if (!dt) return "A";
                var date = new Date(dt);
                var hour = date.getHours();
                var min = date.getMinutes();
                var totalMin = hour * 60 + min;                
                if (totalMin >= 360 && totalMin < 840) {
                    return "A";
                }                
                if (totalMin >= 840 && totalMin < 1320) {
                    return "B";
                }                
                return "C";
            }
