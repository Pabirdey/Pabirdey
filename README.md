        <form method="post">
            <div class="table-responsive" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:15px;">
                <table class="table table-bordered text-center" style="border:2px solid black;">
                    <thead style="border:2px solid black;">
                        <tr>
                            <th>Furnace</th>
                            <th>Actual On Date</th>
                            <th>Actual To Date</th>
                            <th>Reported On Date</th>
                            <th>Reported To Date</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AF_ActOnDate()" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AF_ActToDate()" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AF_ReportOnDate()" onblur="Calc_CBF_ReportOnDate()" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AF_ReportToDate()" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AF_Balance()" name="CBF_Balance" id="CBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="EBF_Furnace" id="EBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AF_ActOnDate()" name="EBF_ActOnDate" id="EBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AF_ActToDate()" name="EBF_ActToDate" id="EBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AF_ReportOnDate()" onblur="Calc_EBF_ReportOnDate()" name="EBF_ReportOnDate" id="EBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AF_ReportToDate()" name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AF_Balance()" name="EBF_Balance" id="EBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="FBF_Furnace" id="FBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AF_ActOnDate()" name="FBF_ActOnDate" id="FBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AF_ActTDate()" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AF_ReportOnDate()" onblur="Calc_FBF_ReportOnDate()" name="FBF_ReportOnDate" id="FBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AF_ReportToDate()" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AF_Balance()" name="FBF_Balance" id="FBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="GBF_Furnace" id="GBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AG_ActOnDate()" name="GBF_ActOnDate" id="GBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AG_ActToDate()"name="GBF_ActToDate" id="GBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AG_ReportOnDate()" onblur="Calc_GBF_ReportOnDate()" name="GBF_ReportOnDate" id="GBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AG_ReportToDate()" name="GBF_ReportToDate" id="GBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AG_Balance()" name="GBF_Balance" id="GBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="HBF_Furnace" id="HBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AH_ActOnDate()" name="HBF_ActOnDate" id="HBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AH_ActToDate()" name="HBF_ActToDate" id="HBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AH_ReportOnDate()" onblur="Calc_HBF_ReportOnDate()" name="HBF_ReportOnDate" id="HBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AH_ReportToDate()" name="HBF_ReportToDate" id="HBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AH_Balance()" name="HBF_Balance" id="HBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="IBF_Furnace" id="IBF_Furnace" /></td>
                            <td><input class="form-control" type="text" value="@Model.ACT_ONDT" oninput="Calc_AI_ActOnDate()" name="IBF_ActOnDate" id="IBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" oninput="Calc_AI_ActToDate()" name="IBF_ActToDate" id="IBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" oninput="Calc_AI_ReportOnDate()" onblur="Calc_IBF_ReportOnDate()" name="IBF_ReportOnDate" id="IBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" oninput="Calc_AI_ReportToDate()" name="IBF_ReportToDate" id="IBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.BALANCE" oninput="Calc_AI_Balance()" name="IBF_Balance" id="IBF_Balance" /></td>
                        </tr>
                        <tr>                           
                            <td>A-F</td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ActOnDate" id="CtoFBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text"  name="CtoFBF_ActToDate" id="CtoFBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ReportOnDate" id="CtoFBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_ReportToDate" id="CtoFBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly  name="CtoFBF_Balance" id="CtoFBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td>A-G</td>
                            <td><input class="form-control" type="text" readonly name="CtoGBF_ActOnDate" id="CtoGBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" name="CtoGBF_ActToDate" id="CtoGBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoGBF_ReportOnDate" id="CtoGBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoGBF_ReportToDate" id="CtoGBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoGBF_Balance" id="CtoGBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td>A-H</td>
                            <td><input class="form-control" type="text" readonly name="CtoHBF_ActOnDate" id="CtoHBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" name="CtoHBF_ActToDate" id="CtoHBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoHBF_ReportOnDate" id="CtoHBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoHBF_ReportToDate" id="CtoHBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoHBF_Balance" id="CtoHBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td>A-I</td>
                            <td><input class="form-control" type="text" readonly name="CtoIBF_ActOnDate" id="CtoIBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" name="CtoIBF_ActToDate" id="CtoIBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoIBF_ReportOnDate" id="CtoIBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoIBF_ReportToDate" id="CtoIBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly name="CtoIBF_Balance" id="CtoIBF_Balance" /></td>
                        </tr>
                    </tbody>
                </table>
              </div>

                <!-- ===================== ACTUAL BREAKUP ===================== -->
                <h5 class="mt-4 mb-3 fw-bold border-bottom pb-2" style="font-family:Allan,cursive;">Actual Breakup</h5>
                <div class="table-responsive">
                    <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;font-weight:bold;border:2px solid black;">
                        <thead>
                            <tr>
                                <th></th>
                                <th>LD1 Tons</th>
                                <th>LD2 Tons</th>
                                <th>LD3 Tons</th>
                                <th>MRD TP Tons</th>                                
                            </tr>
                        </thead>
                        <tbody style="font-family:Courier New, Courier, monospace;">
                            <tr>
                                <td><label>On Date</label></td>
                                <td><input class="form-control" type="text" readonly value="@Model.A_F_LD1_TONS" name="A_F_LD1_TONS" id="A_F_LD1_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.A_F_LD2_TONS"  name="A_F_LD2_TONS" id="A_F_LD2_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.A_F_LD3_TONS" name="A_F_LD3_TONS" id="A_F_LD3_TONS" /></td>
                                <td><input class="form-control" type="text" value="@Model.A_F_MRD_TP_TONS" name="A_F_MRD_TP_TONS" id="A_F_MRD_TP_TONS" /></td>                               
                                
                            </tr>
                            <tr>
                                <td><label>To Date A-F</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD1_TONS" name="A_F_ACT_LD1_TONS" id="A_F_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD2_TONS" name="A_F_ACT_LD2_TONS" id="A_F_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" type="text" value="@Model.ACT_LD3_TONS" name="A_F_ACT_LD3_TONS" id="A_F_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_MRD_TP_TONS" name="A_F_ACT_MRD_TP_TONS" id="A_F_ACT_MRD_TP_TONS" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-G</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD1_TONS" name="A_G_ACT_LD1_TONS" id="A_G_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD2_TONS" name="A_G_ACT_LD2_TONS" id="A_G_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" type="text" value="@Model.ACT_LD3_TONS" name="A_G_ACT_LD3_TONS" id="A_G_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_MRD_TP_TONS" name="A_G_ACT_MRD_TP_TONS" id="A_G_ACT_MRD_TP_TONS" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-H</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD1_TONS" name="A_H_ACT_LD1_TONS" id="A_H_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD2_TONS" name="A_H_ACT_LD2_TONS" id="A_H_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" type="text" value="@Model.ACT_LD3_TONS" name="A_H_ACT_LD3_TONS" id="A_H_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_MRD_TP_TONS" name="A_H_ACT_MRD_TP_TONS" id="A_H_ACT_MRD_TP_TONS" /></td>                                
                            </tr>
                            <tr>
                                <td><label>To Date A-I</label></td>                                
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD1_TONS" name="A_I_ACT_LD1_TONS" id="A_I_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_LD2_TONS" name="A_I_ACT_LD2_TONS" id="A_I_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" type="text" value="@Model.ACT_LD3_TONS" name="A_I_ACT_LD3_TONS" id="A_I_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" type="text" readonly value="@Model.ACT_MRD_TP_TONS" name="A_I_ACT_MRD_TP_TONS" id="A_I_ACT_MRD_TP_TONS" /></td>                                
                            </tr>
                        </tbody>
                    </table>
                </div>
                <!-- Buttons -->
                <div class="text-center mt-3">
                    <button class="btn btn-success btn-sm">Save</button>
                    <button class="btn btn-info btn-sm">Back</button>
                    <button class="btn btn-primary btn-sm">Raw Mat Cons</button>
                    <button class="btn btn-success btn-sm">Calc_ Now</button>
                </div>
</form>
