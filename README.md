 function Display_CTOFBFReportData(fDate) {
        $.ajax({
            url: '@Url.Action("GetCTOFBFReportDataByFurnace", "HML")',
            type: 'GET',
            data: { fDate: fDate },
            success: function (data) {
                if (data.message) {
                    alert(data.message);
                    return;
                }
                data.forEach(function (item) {
                    if (item.FURNACE === "C") {
                        $("#CBF_Furnace").val(item.FURNACE);
                        $("#CBF_ActOnDate").val(item.ACT_ONDT);
                        $("#CBF_ActToDate").val(item.ACT_TODT);
                        $("#CBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#CBF_ReportToDate").val(item.REPORT_TODT);
                        $("#CBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "E") {
                        $("#EBF_Furnace").val(item.FURNACE);
                        $("#EBF_ActOnDate").val(item.ACT_ONDT);
                        $("#EBF_ActToDate").val(item.ACT_TODT);
                        $("#EBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#EBF_ReportToDate").val(item.REPORT_TODT);
                        $("#EBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "F") {
                        $("#FBF_Furnace").val(item.FURNACE);
                        $("#FBF_ActOnDate").val(item.ACT_ONDT);
                        $("#FBF_ActToDate").val(item.ACT_TODT);
                        $("#FBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#FBF_ReportToDate").val(item.REPORT_TODT);
                        $("#FBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "G") {
                        $("#GBF_Furnace").val(item.FURNACE);
                        $("#GBF_ActOnDate").val(item.ACT_ONDT);
                        $("#GBF_ActToDate").val(item.ACT_TODT);
                        $("#GBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#GBF_ReportToDate").val(item.REPORT_TODT);
                        $("#GBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "H") {
                        $("#HBF_Furnace").val(item.FURNACE);
                        $("#HBF_ActOnDate").val(item.ACT_ONDT);
                        $("#HBF_ActToDate").val(item.ACT_TODT);
                        $("#HBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#HBF_ReportToDate").val(item.REPORT_TODT);
                        $("#HBF_Balance").val(item.BALANCE);
                    }
                    if (item.FURNACE === "I") {
                        $("#IBF_Furnace").val(item.FURNACE);
                        $("#IBF_ActOnDate").val(item.ACT_ONDT);
                        $("#IBF_ActToDate").val(item.ACT_TODT);
                        $("#IBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#IBF_ReportToDate").val(item.REPORT_TODT);
                        $("#IBF_Balance").val(item.BALANCE);
                    }
                });
<tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActToDate()" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate(); Calc_CBF_ReportOnDate();" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate(); Calc_CBF_ReportOnDate();" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="CBF_Balance" id="CBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="EBF_Furnace" id="EBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="EBF_ActOnDate" id="EBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActToDate()" name="EBF_ActToDate" id="EBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()"  name="EBF_ReportOnDate" id="EBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()"  name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="EBF_Balance" id="EBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="FBF_Furnace" id="FBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="FBF_ActOnDate" id="FBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActTDate()" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()"   name="FBF_ReportOnDate" id="FBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="FBF_Balance" id="FBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="GBF_Furnace" id="GBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AG_ActOnDate()" name="GBF_ActOnDate" id="GBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AG_ActToDate()"name="GBF_ActToDate" id="GBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AG_ReportOnDate()"  name="GBF_ReportOnDate" id="GBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AG_ReportToDate()" name="GBF_ReportToDate" id="GBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AG_Balance()" name="GBF_Balance" id="GBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="HBF_Furnace" id="HBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AH_ActOnDate()" name="HBF_ActOnDate" id="HBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AH_ActToDate()" name="HBF_ActToDate" id="HBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AH_ReportOnDate()"  name="HBF_ReportOnDate" id="HBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AH_ReportToDate()" name="HBF_ReportToDate" id="HBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AH_Balance()" name="HBF_Balance" id="HBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="IBF_Furnace" id="IBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AI_ActOnDate()" name="IBF_ActOnDate" id="IBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AI_ActToDate()" name="IBF_ActToDate" id="IBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AI_ReportOnDate()"  name="IBF_ReportOnDate" id="IBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AI_ReportToDate()" name="IBF_ReportToDate" id="IBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AI_Balance()" name="IBF_Balance" id="IBF_Balance" /></td>
                        </tr>
