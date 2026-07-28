 <div class="col-md-5">
                        <div class="section-box">
                            <div class="section-title">Production Breakup</></div>
                            <div class="table-responsive" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:15px;">
                                <table class="table table-bordered text-center">
                                    <thead>
                                        <tr>
                                            <th style="width:35px;">Furnace</th>
                                            <th>Actual OnDate</th>
                                            <th>Actual ToDate</th>
                                            <th>Reported OnDate</th>
                                            <th>Reported ToDate</th>
                                            <th>Balance</th>
                                        </tr>
                                    </thead>                                   
                                    <tbody>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_C" readonly value="C" /></td>                                            <td><input type="text" class="form-control" id="ACTUAL_C" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_C_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_C" id="REPORTED_C" onblur="TotCTOF()"/></td>
                                            <td><input type="text" class="form-control" id="REPORTED_C_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="BALANCE_C" readonly /></td>                                           
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_D" readonly value="D" /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_D" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_D_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_D" id="REPORTED_D" onblur="TotCTOF()" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_D_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="BALANCE_D" readonly /></td>
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_E" readonly value="E" /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_E" id="REPORTED_E" onblur="TotCTOF()" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="BALANCE_E" readonly /></td> 
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="FURNACE_F" readonly value="F"/></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_F" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_F_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_F" id="REPORTED_F" onblur="TotCTOF()"/></td>
                                            <td><input type="text" class="form-control" id="REPORTED_F_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="BALANCE_F" readonly /></td> 
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="TXT_FURNACE_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_G_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_G" id="TXT_RPT_G"/></td>
                                            <td><input type="text" class="form-control" id="TXT_RPT_G_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="TXT_BAL_G" readonly /></td>
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="TXT_FURNACE_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_H_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_H" id="TXT_RPT_H" /></td>
                                            <td><input type="text" class="form-control" id="TXT_RPT_H_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="TXT_BAL_H" readonly /></td>
                                        </tr>
                                        <tr>
                                            <td><input type="text" class="form-control" id="TXT_FURNACE_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_ACTUAL_I_TD" readonly /></td>
                                            <td><input type="text" class="form-control reported_I" id="TXT_RPT_I" /></td>
                                            <td><input type="text" class="form-control" id="TXT_RPT_I_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="TXT_BAL_I" readonly /></td>
                                        </tr>   
                                        <tr>                                            
                                            <td><input type="text" class="form-control"  readonly value="A-F"/></td>
                                            <td><input type="text" class="form-control" id="DisplayActual" readonly /></td>
                                            <td><input type="text" class="form-control" id="DisplayActual_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="DisplayReported" readonly /></td>
                                            <td><input type="text" class="form-control" id="DisplayReported_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="DisplayBalance" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="A-G" /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_G_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_G_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="DISPLAY_BAL_G" readonly /></td>
                                        </tr>                                        
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="A-H" /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_H_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_H_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="DISPLAY_BAL_H" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="A-I" /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_ACT_I_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="DISPLAY_RPT_I_TD" readonly /></td>
                                            <td><input type="text" class="form-control" style="text-align:right" id="DISPLAY_BAL_I" readonly /></td>
                                        </tr>                                                                 
                                    </tbody>
                                </table>

                            </div>
                        </div>                 
                 </div>
                    <div class="col-md-5">
                        <div class="section-box">
                            <div class="section-title">Actual Breakup</></div>
                            <div class="table-responsive" style="font-family:'Courier New', Courier, monospace;font-weight:bold;font-size:15px;">
                                <table class="table table-bordered text-center">
                                    <thead>
                                        <tr>   
                                            <th style="width:130px;"></th>                                         
                                            <th>LD1 Tons</th>
                                            <th>LD2 Tons</th>
                                            <th>LD3 Tons</th>
                                            <th>MRD TP Tons</th>                                            
                                        </tr>
                                    </thead>
                                    <tbody>                                      
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="A-F On date" /></td>
                                            <td><input type="text" class="form-control" id="TXTCTOFLD1TONS" readonly/></td>
                                            <td><input type="text" class="form-control" id="TXTCTOFLD2TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTCTOFLD3TONS" readonly/></td>
                                            <td><input type="text" class="form-control" id="TXTCTOFMRDTPTONS" readonly /></td>                                            
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="GBF On date" /></td>
                                            <td><input type="text" class="form-control" id="TXTGBFLD1TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTGBFLD2TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTGBFLD3TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTGBFMRDTPTONS" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="HBF On date" /></td>
                                            <td><input type="text" class="form-control" id="TXTHBFLD1TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTHBFLD2TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTHBFLD3TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTHBFMRDTPTONS" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="IBF On date" /></td>
                                            <td><input type="text" class="form-control" id="TXTIBFLD1TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTIBFLD2TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTIBFLD3TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXTIBFMRDTPTONS" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date A-F" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS_ACTUAL_TD_A_F" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS_ACTUAL_TD_A_F" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS_ACTUAL_TD_A_F" readonly/></td>
                                            <td><input type="text" class="form-control" id="TXT_MRD_TONS_ACTUAL_TD_A_F" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date G" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS_ACTUAL_TD_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS_ACTUAL_TD_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS_ACTUAL_TD_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_MRD_TONS_ACTUAL_TD_G" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date H" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS_ACTUAL_TD_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS_ACTUAL_TD_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS_ACTUAL_TD_H" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_MRD_TONS_ACTUAL_TD_H" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date I" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS_ACTUAL_TD_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS_ACTUAL_TD_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS_ACTUAL_TD_I" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_MRD_TONS_ACTUAL_TD_I" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date A-G" /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOG_LD1_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOG_LD2_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOG_LD3_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOG_MRDTP_TONS" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date A-H" /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOH_LD1_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOH_LD2_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOH_LD3_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOH_MRDTP_TONS" readonly /></td>
                                        </tr>
                                        <tr>                                            
                                            <td><input type="text" class="form-control" readonly value="TO Date A-I" /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOI_LD1_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOI_LD2_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOI_LD3_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_CTOI_MRDTP_TONS" readonly /></td>
                                        </tr>
                                        <tr class="LD_A_F">
                                            <td><input type="text" class="form-control" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_MRDTP_TONS" readonly /></td>                                            
                                        </tr>
                                        <tr class="LD_G">
                                            <td><input type="text" class="form-control" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD1_TONS_G" /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD2_TONS_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_LD3_TONS_G" readonly /></td>
                                            <td><input type="text" class="form-control" id="TXT_MRDTP_TONS_G" readonly /></td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                        <!-- ================= RIGHT TABLE ================= -->
                        <div class="btn-box-wrapper">
                            <div class="btn-box">
                                <button type="button" class="btn btn-success SabeBFProd" onclick="SaveBFProdData()">
                                    Save
                                </button>
                                <button type="button"  class="btn btn-primary CallProcedure" onclick="BFProdProcedure()">
                                    Calculate Now
                                </button>                           
                                @Html.ActionLink("Raw Mat Cons", "BF_RawMaterial_Consumption", "BF_Production", null, new { @class = "btn btn-warning RawMatCons"})
                                @Html.ActionLink("Back", "HML_Home", "HML", new { bf = @urlBF }, new { @class = "btn btn-primary Backbtn" })
                            </div>
                        </div>
                    </div>
                    <div class="col-md-2">                                                                        
                        <input type="text" class="form-control NOOFTP_G" id="NOOFTP_G" style="margin-top:80px;margin-top:80px;width:80px;" />
                        <input type="text" class="form-control NOOFTP_G" id="NOOFTP_G" style="margin-top:80px;margin-top:80px;width:80px;" />
                    </div>  
