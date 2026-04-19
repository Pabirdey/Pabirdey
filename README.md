<td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActToDate()" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate(); Calc_CBF_ReportOnDate();" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate(); Calc_CBF_ReportOnDate();" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="CBF_Balance" id="CBF_Balance" /></td>
