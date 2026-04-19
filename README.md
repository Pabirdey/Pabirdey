  <form method="post">
            <div class="row">
                <!-- ================= LEFT TABLE ================= -->
                <div class="col-md-6">
                    <div class="table-responsive">
                        <table class="table table-bordered text-center"
                               style="border:2px solid black;font-family:'Courier New';font-weight:bold;">
                            <thead>
                                <tr>
                                    <th style="width:18px;">Furnace</th>
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
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()" name="EBF_ReportOnDate" id="EBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()" name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="EBF_Balance" id="EBF_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="FBF_Furnace" id="FBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="FBF_ActOnDate" id="FBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActTDate()" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()" name="FBF_ReportOnDate" id="FBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="FBF_Balance" id="FBF_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="GBF_Furnace" id="GBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AG_ActOnDate()" name="GBF_ActOnDate" id="GBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AG_ActToDate()" name="GBF_ActToDate" id="GBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AG_ReportOnDate()" name="GBF_ReportOnDate" id="GBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AG_ReportToDate()" name="GBF_ReportToDate" id="GBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AG_Balance()" name="GBF_Balance" id="GBF_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="HBF_Furnace" id="HBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AH_ActOnDate()" name="HBF_ActOnDate" id="HBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AH_ActToDate()" name="HBF_ActToDate" id="HBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AH_ReportOnDate()" name="HBF_ReportOnDate" id="HBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AH_ReportToDate()" name="HBF_ReportToDate" id="HBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AH_Balance()" name="HBF_Balance" id="HBF_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="IBF_Furnace" id="IBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AI_ActOnDate()" name="IBF_ActOnDate" id="IBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AI_ActToDate()" name="IBF_ActToDate" id="IBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AI_ReportOnDate()" name="IBF_ReportOnDate" id="IBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AI_ReportToDate()" name="IBF_ReportToDate" id="IBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AI_Balance()" name="IBF_Balance" id="IBF_Balance" /></td>
                                </tr>
                                <tr>
                                    <td>A-F</td>
                                    <td><input class="form-control" type="text" readonly name="CtoFBF_ActOnDate" id="CtoFBF_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly name="CtoFBF_ActToDate" id="CtoFBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" readonly name="CtoFBF_ReportOnDate" id="CtoFBF_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly name="CtoFBF_ReportToDate" id="CtoFBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly name="CtoFBF_Balance" id="CtoFBF_Balance" /></td>
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
                </div>
                <!-- ================= RIGHT TABLE ================= -->
                <div class="col-md-6">
                    @*<h5 style="font-family:Allan,cursive;">Actual Breakup</h5>*@
                    <div class="table-responsive">
                        <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;font-weight:bold;border:2px solid black;">
                            <thead>
                                <tr>
                                    <th style="width:120px;"></th>
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
                                    <td><input class="form-control" type="text" readonly value="@Model.A_F_LD2_TONS" name="A_F_LD2_TONS" id="A_F_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.A_F_LD3_TONS" name="A_F_LD3_TONS" id="A_F_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.A_F_MRD_TP_TONS" name="A_F_MRD_TP_TONS" id="A_F_MRD_TP_TONS" /></td>

                                </tr>
                                @*<tr>
                                    <td><label>G On Date</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.G_LD1_TONS" name="G_LD1_TONS" id="G_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.G_LD2_TONS" name="G_LD2_TONS" id="G_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.G_LD3_TONS" name="G_LD3_TONS" id="G_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.G_MRD_TP_TONS" name="G_MRD_TP_TONS" id="G_MRD_TP_TONS" /></td>

                                </tr>*@
                                @*<tr>
                                    <td><label>(H)On Date</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.H_LD1_TONS" name="H_LD1_TONS" id="H_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.H_LD2_TONS" name="H_LD2_TONS" id="H_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.H_LD3_TONS" name="H_LD3_TONS" id="H_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.H_MRD_TP_TONS" name="H_MRD_TP_TONS" id="H_MRD_TP_TONS" /></td>

                                </tr>
                                <tr>
                                    <td><label>(I)On Date</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.I_LD1_TONS" name="I_LD1_TONS" id="I_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.I_LD2_TONS" name="I_LD2_TONS" id="I_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.I_LD3_TONS" name="I_LD3_TONS" id="I_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.I_MRD_TP_TONS" name="I_MRD_TP_TONS" id="I_MRD_TP_TONS" /></td>

                                </tr>*@
                                <tr>
                                    <td><label>ToDate A-F</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_F_TODT_LD1_TONS" name="ACT_A_F_TODT_LD1_TONS" id="ACT_A_F_TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_F_TODT_LD2_TONS" name="ACT_A_F_TODT_LD2_TONS" id="ACT_A_F_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_A_F_TODT_LD3_TONS" name="ACT_A_F_TODT_LD3_TONS" id="ACT_A_F_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_F_TODT_MRD_TP_TONS" name="ACT_A_F_TODT_MRD_TP_TONS" id="ACT_A_F_TODT_MRD_TP_TONS" /></td>
                                </tr>
                                @*<tr>
                                    <td><label>ToDate G</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_G_TODT_LD1_TONS" name="ACT_G_TODT_LD1_TONS" id="ACT_G__TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_G_TODT_LD2_TONS" name="ACT_G_TODT_LD2_TONS" id="ACT_G_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_G_TODT_LD3_TONS" name="ACT_G_TODT_LD3_TONS" id="ACT_G_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_G_TODT_MRD_TP_TONS" name="ACT_G_TODT_MRD_TP_TONS" id="ACT_G_TODT_MRD_TP_TONS" /></td>
                                </tr>*@
                                @*<tr>
                                    <td><label>To Date H</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_H_TODT_LD1_TONS" name="ACT_H_TODT_LD1_TONS" id="ACT_H__TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_H_TODT_LD2_TONS" name="ACT_H_TODT_LD2_TONS" id="ACT_H_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_H_TODT_LD3_TONS" name="ACT_H_TODT_LD3_TONS" id="ACT_H_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_H_TODT_MRD_TP_TONS" name="ACT_H_TODT_MRD_TP_TONS" id="ACT_H_TODT_MRD_TP_TONS" /></td>
                                </tr>
                                <tr>
                                    <td><label>To Date I</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_I_TODT_LD1_TONS" name="ACT_I_TODT_LD1_TONS" id="ACT_I__TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_I_TODT_LD2_TONS" name="ACT_I_TODT_LD2_TONS" id="ACT_I_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_I_TODT_LD3_TONS" name="ACT_I_TODT_LD3_TONS" id="ACT_I_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_MRD_TP_TONS" name="ACT_MRD_TP_TONS" id="ACT_MRD_TP_TONS" /></td>
                                </tr>*@
                                <tr>
                                    <td><label>ToDate A-G</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_G_TODT_LD1_TONS" name="ACT_A_G_TODT_LD1_TONS" id="ACT_A_G_TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_G_TODT_LD2_TONS" name="ACT_A_G_TODT_LD2_TONS" id="ACT_A_G_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_A_G_TODT_LD3_TONS" name="ACT_A_G_TODT_LD3_TONS" id="ACT_A_G_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_G_TODT_MRD_TP_TONS" name="ACT_A_G_TODT_MRD_TP_TONS" id="ACT_A_G_TODT_MRD_TP_TONS" /></td>
                                </tr>
                                <tr>
                                    <td><label>ToDate A-H</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_H_TODT_LD1_TONS" name="ACT_A_H_TODT_LD1_TONS" id="ACT_A_H_TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_H_TODT_LD2_TONS" name="ACT_A_H_TODT_LD2_TONS" id="ACT_A_H_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_A_H_TODT_LD3_TONS" name="ACT_A_H_TODT_LD3_TONS" id="ACT_A_H_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_H_TODT_MRD_TP_TONS" name="ACT_A_H_TODT_MRD_TP_TONS" id="ACT_A_H_TODT_MRD_TP_TONS" /></td>
                                </tr>
                                <tr>
                                    <td><label>ToDate A-I</label></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_I_TODT_LD1_TONS" name="ACT_A_I_TODT_LD1_TONS" id="ACT_A_I_TODT_LD1_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_I_TODT_LD2_TONS" name="ACT_A_I_TODT_LD2_TONS" id="ACT_A_I_TODT_LD2_TONS" /></td>
                                    <td><input class="form-control" type="text" value="@Model.ACT_A_I_TODT_LD3_TONS" name="ACT_A_I_TODT_LD3_TONS" id="ACT_A_I_TODT_LD3_TONS" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_A_I_TODT_MRD_TP_TONS" name="ACT_A_I_TODT_MRD_TP_TONS" id="ACT_A_I_TODT_MRD_TP_TONS" /></td>
                                </tr>
                            </tbody>
                        </table>
                        <div>
                            <div style="margin-top:100px;margin-left:160px;">
                                <button class="btn btn-success" onclick="SaveProd()">Save</button>
                                <button class="btn btn-primary" onclick="Calculate()">Calculate</button>
                                <button class="btn btn-warning" onclick="RawMatCons()">Raw Mat Cons</button>
                            </div>
                        </div>
                    </div>
            </div>           
        </div>
      </form>
