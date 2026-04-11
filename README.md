  <form method="post">
            <div class="table-responsive" style="font-family:Allan,cursive;font-weight:bold;font-size:15px;">
                <table class="table table-bordered text-center" style="border:2px solid black;">
                    <thead style="border:2px solid black;">
                        <tr>                           
                            <th>Furnace</th>
                            <th>On Date</th>
                            <th>To Date</th>
                            <th>On Date</th>
                            <th>To Date</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>                        
                        <tr>                            
                            <td><input class="form-control" type="text" readonly value="@Model.CBF_Furnace" name="CBF_Furnace" id="CBF_Furnace"/></td>
                            <td><input class="form-control" type="text" readonly value="@Model.CBF_ActOnDate" name="CBF_ActOnDate" id="CBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.CBF_ActToDate" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                            <td><input class="form-control" type="text"  value="@Model.CBF_ReportOnDate" name="CBF_ReportOnDate" id="CBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.CBF_ReportToDate" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>                            
                            <td><input class="form-control" type="text" readonly value="@Model.CBF_Balance" name="CBF_Balance" id="CBF_Balance" /></td>  
                        </tr>                        
                        <tr>                            
                            <td><input class="form-control" type="text" readonly value="@Model.EBF_Furnace" name="EBF_Furnace" id="EBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.EBF_ActOnDate" name="EBF_ActOnDate" id="EBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.EBF_ActToDate" name="EBF_ActToDate" id="EBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.EBF_ReportOnDate" name="EBF_ReportOnDate" id="EBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.EBF_ReportToDate" name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.EBF_Balance" name="EBF_Balance" id="EBF_Balance" /></td>  
                        </tr>                        
                        <tr>                            
                            <td><input class="form-control" type="text" readonly value="@Model.FBF_Furnace" name="FBF_Furnace" id="FBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.FBF_ActOnDate" name="FBF_ActOnDate" id="FBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.FBF_ActToDate" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.FBF_ReportOnDate" name="FBF_ReportOnDate" id="FBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.FBF_ReportToDate" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.FBF_Balance" name="FBF_Balance" id="FBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.GBF_Furnace" name="GBF_Furnace" id="GBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.GBF_ActOnDate" name="GBF_ActOnDate" id="GBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.GBF_ActToDate" name="GBF_ActToDate" id="GBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.GBF_ReportOnDate" name="GBF_ReportOnDate" id="GBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.GBF_ReportToDate" name="GBF_ReportToDate" id="GBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.GBF_Balance" name="GBF_Balance" id="GBF_Balance" /></td>                            
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.HBF_Furnace" name="HBF_Furnace" id="HBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.HBF_ActOnDate" name="HBF_ActOnDate" id="HBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.HBF_ActToDate" name="HBF_ActToDate" id="HBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.HBF_ReportOnDate" name="HBF_ReportOnDate" id="HBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.HBF_ReportToDate" name="HBF_ReportToDate" id="HBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.HBF_Balance" name="HBF_Balance" id="HBF_Balance" /></td>
                        </tr>
                        <tr>
                            <td><input class="form-control" type="text" readonly value="@Model.IBF_Furnace" name="IBF_Furnace" id="IBF_Furnace" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.IBF_ActOnDate" name="IBF_ActOnDate" id="IBF_ActOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.IBF_ActToDate" name="IBF_ActToDate" id="IBF_ActToDate" /></td>
                            <td><input class="form-control" type="text" value="@Model.IBF_ReportOnDate" name="IBF_ReportOnDate" id="IBF_ReportOnDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.IBF_ReportToDate" name="IBF_ReportToDate" id="IBF_ReportToDate" /></td>
                            <td><input class="form-control" type="text" readonly value="@Model.IBF_Balance" name="IBF_Balance" id="IBF_Balance" /></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- ===================== ACTUAL BREAKUP ===================== -->
            <h5 class="mt-4 mb-3 fw-bold border-bottom pb-2" style="font-family:Allan,cursive;">Actual Breakup</h5>
            <div class="table-responsive">
                <table class="table table-bordered table-hover text-center align-middle" style="font-family:'Courier New', Courier, monospace;">
                    <thead>
                        <tr>
                            <th></th>
                            <th>LD1 Tons</th>
                            <th>LD2 Tons</th>
                            <th>LD3 Tons</th>
                            <th>MRD TP Tons</th>
                            <th>No of TP</th>
                            <th>No of Slag Ladle</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
            <!-- Buttons -->
            <div class="text-center mt-3">
                <button class="btn btn-success btn-sm">Save</button>
                <button class="btn btn-info btn-sm">Back</button>
                <button class="btn btn-primary btn-sm">Raw Mat Cons</button>
                <button class="btn btn-success btn-sm">Calculate Now</button>
            </div>
            </form>
