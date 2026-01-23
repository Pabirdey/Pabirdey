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
         <script type="text/javascript">
    let lsSelectedFDate;
    let IsSelectedFur;

    $(document).ready(function () {

        lsSelectedFDate = '@DateTime.Today.ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';

        $('#tbFDatePick').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).val(lsSelectedFDate);

        $('#tbFDatePick').on('changeDate', function () {
            lsSelectedFDate = $('#tbFDatePick').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

        $('#lstFur').change(function () {
            IsSelectedFur = $('#lstFur option:selected').val();
            Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
        });

    });

    function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {

        $.ajax({
            url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
            type: 'GET',
            data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
            success: function (result) {

                let parsedData = JSON.parse(result);
                let tableBody = "";

                for (let i = 0; i < parsedData.length; i++) {
                    
                    let backFire = (parsedData[i].BACK_FIRE || '').toString().trim().toUpperCase();
                    let clayLeak = (parsedData[i].CLAY_LEAKAGE || '').toString().trim().toUpperCase();

                    tableBody += `<tr data-castno="${parsedData[i].CAST_NO}">`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].CAST_NO}" readonly />
                    </td>`;

                    tableBody += `<td>
                        <select class="form-select form-select-lg">
                            <option value=""></option>
                            <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                            <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                        </select>
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].MG_CLAY_USED || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].LOT_NO || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].NO_OF_BAGS || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].MUDGUN_HOLD_TIME || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <select class="form-select form-select-lg">
                            <option value=""></option>
                            <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>REPLACEMENT</option>
                            <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>WEILD</option>
                        </select>
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].MNOZZLE_BEF_CLOSING || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].MNOZZLE_AFT_CLOSING || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].INIT_PLUGIN_PRESSURE || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].MAX_PLUGIN_PRESSURE || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].FINAL_PLUGIN_PRESSURE || ''}" />
                    </td>`;

                    tableBody += `<td>
                        <input class="form-control form-control-lg" value="${parsedData[i].PRESS_ON_FORCE || ''}" />
                    </td>`;                    
                    tableBody += `<td>
                        <select class="form-select form-select-lg">
                            <option value=""></option>
                            <option ${(clayLeak === 'YES' || clayLeak === 'Y') ? 'selected' : ''}>YES</option>
                            <option ${(clayLeak === 'NO'  || clayLeak === 'N') ? 'selected' : ''}>NO</option>
                        </select>
                    </td>`;                    
                    tableBody += `<td>
                        <select class="form-select form-select-lg">
                            <option value=""></option>
                            <option ${(backFire === 'YES' || backFire === 'Y') ? 'selected' : ''}>YES</option>
                            <option ${(backFire === 'NO'  || backFire === 'N') ? 'selected' : ''}>NO</option>
                        </select>
                    </td>`;

                    tableBody += `</tr>`;
                }

                $("#Mudgun_Details tbody").html(tableBody);
            }
        });
    }
</script>
