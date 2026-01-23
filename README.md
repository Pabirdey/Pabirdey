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

                    // 🔹 Normalize values (VERY IMPORTANT)
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

                    /* ✅ CLAY LEAKAGE */
                    tableBody += `<td>
                        <select class="form-select form-select-lg">
                            <option value=""></option>
                            <option ${(clayLeak === 'YES' || clayLeak === 'Y') ? 'selected' : ''}>YES</option>
                            <option ${(clayLeak === 'NO'  || clayLeak === 'N') ? 'selected' : ''}>NO</option>
                        </select>
                    </td>`;

                    /* ✅ BACK FIRE (FIXED) */
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