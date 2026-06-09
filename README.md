 [HttpPost]
        public ActionResult CalculateLadle(Granshot model)
        {
            try
            {
                decimal v_Pouring_rate = 0;
                int v_lfe_time;
                DateTime v_timestamp;                
                DateTime baseDate = DateTime.Parse(model.lsSelectedFDate);                
                DateTime startTime = DateTime.Parse(model.LADLE_FLST_TIME);
                DateTime endTime = DateTime.Parse(model.LADLE_FLEND_TIME);
                v_lfe_time = endTime.Hour;                
                if (v_lfe_time >= 6 && v_lfe_time < 14)
                {
                    if (model.ddlshift == "C")
                        v_timestamp = baseDate.AddDays(1);
                    else
                        v_timestamp = baseDate;
                }
                else if (v_lfe_time >= 14 && v_lfe_time < 22)
                {
                    v_timestamp = baseDate;
                }
                else if (v_lfe_time >= 22)
                {
                    v_timestamp = baseDate;
                }
                else
                {
                    v_timestamp = baseDate.AddDays(1);
                }

                model.GROSS_WT = GetGrossWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
                model.TARE_WT = GetTareWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
                model.NET_WT = GetNetWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
                model.HMT = GetHmt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
                var minutes = (endTime - startTime).TotalMinutes;

                if (minutes > 0)
                    model.POURING_RATE = model.NET_WT / (decimal)minutes;
                else
                    model.POURING_RATE = 0;

                v_Pouring_rate = model.POURING_RATE;

                return Json(new
                {
                    success = true,
                    data = model
                });
            }
            catch (Exception ex)
            {
                return Json(new
                {
                    success = false,
                    message = ex.Message
                });
            }
        }
         function BindTable(data) {            
            $("#tblBody").empty();
            var totalRows = 15;
            var dataCount = data.length;
            if (dataCount > 0) {
                $.each(data, function (i, item) {
                    var row = `<tr>
                <td><input type="text" class="table-input" value="${item.CAST_NO || ''}"readonly></td>
                <td>
                <input type="time" class ="table-input" value="${item.CAST_ST_TIME || ''}">
                </td>
                <td><input type="time" class="table-input" value="${item.CAST_END_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.TRP_NO || ''}"></td>
                <td><input type="time" class="table-input" value="${item.LADLE_FLST_TIME || ''}"></td>
                <td><input type="time" class="table-input" value="${item.LADLE_FLEND_TIME || ''}"></td>
                <td>
                    <select class ="table-input arrivedFrom">
                        <option value=""></option>
                        <option value="C" ${item.ARRIVED_FROM === 'C' ? 'selected': ''}>C</option>
                        <option value="E" ${item.ARRIVED_FROM === 'E' ? 'selected': ''}>E</option>
                        <option value="F" ${item.ARRIVED_FROM === 'F' ? 'selected': ''}>F</option>
                        <option value="C" ${item.ARRIVED_FROM === 'G' ? 'selected': ''}>G</option>
                        <option value="E" ${item.ARRIVED_FROM === 'H' ? 'selected': ''}>H</option>
                        <option value="F" ${item.ARRIVED_FROM === 'I' ? 'selected': ''}>I</option>
                    </select>
               </td>
               console.log(item.ARRIVED_FROM);
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input"  value="${item.GROSS_WT || ''}"readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" value="${item.TARE_WT || ''}"readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" value="${item.NET_WT || ''}"readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" value="${item.POURING_RATE || ''}"readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" value="${item.HMT || ''}"readonly></td>
                <td><input type="text" class ="table-input" value="${item.REASON_POURING || ''}"></td>
                <td class="seqNoCol"><input type="hidden" class ="table-input seqNo" value="${item.SEQ_NO || ''}"readonly></td>
                <td><button type="button" class ="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(row);
                });

                
                for (var i = dataCount; i < totalRows; i++) {

                    var blankRow = `<tr>
                <td><input type="text" class ="table-input" readonly></td>
                <td><input type="time"  class ="table-input"></td>
                <td><input type="time"  class ="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="time"  class ="table-input"></td>
                <td><input type="time"  class ="table-input"></td>

                <td>
                    <select class ="table-input arrivedFrom">                    
                        <option value=""></option>
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                        <option value="F">G</option>
                        <option value="F">H</option>
                        <option value="F">I</option>
                    </select>
                </td>

                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td><input type="text" class ="table-input"></td>
                <td class ="seqNoCol"><input type="hidden" class ="table-input seqNo" readonly></td>
                <td><button type="button" class="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(blankRow);
                }
            }
            else {

               
                for (var i = 0; i < totalRows; i++) {

                    var blankRow = `<tr>
                <td><input type="text" class ="table-input" readonly></td>
                <td><input type="time" class ="table-input"></td>
                <td><input type="time" class ="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="time" class ="table-input"></td>
                <td><input type="time" class ="table-input"></td>

                <td>
                    <select class ="table-input arrivedFrom">                    
                        <option value=""></option>
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                        <option value="F">G</option>
                        <option value="F">H</option>
                        <option value="F">I</option>
                    </select>
                </td>

                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td style="background-color:#c0f9fa;"><input type="text" class ="table-input" readonly></td>
                <td><input type="text" class="table-input"></td>
                <td class ="seqNoCol"><input type="hidden" class ="table-input seqNo" readonly></td>
                <td><button type="button" class="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(blankRow);
                }
            }
        }
