 <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="CBF_Furnace" id="CBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="C_ActOnDate" id="C_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActToDate()" name="CBF_ActToDate" id="CBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate(); Calc_C_ReportOnDate();" name="C_ReportOnDate" id="C_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate(); Calc_C_ReportOnDate();" name="CBF_ReportToDate" id="CBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="C_Balance" id="C_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="EBF_Furnace" id="EBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="E_ActOnDate" id="E_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActToDate()" name="EBF_ActToDate" id="EBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()" name="E_ReportOnDate" id="E_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()" name="EBF_ReportToDate" id="EBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="E_Balance" id="E_Balance" /></td>
                                </tr>
                                <tr>
                                    <td><input class="form-control" type="text" readonly value="@Model.FURNACE" name="FBF_Furnace" id="FBF_Furnace" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_ONDT" onblur="Calc_AF_ActOnDate()" name="F_ActOnDate" id="F_ActOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.ACT_TODT" onblur="Calc_AF_ActTDate()" name="FBF_ActToDate" id="FBF_ActToDate" /></td>
                                    <td><input class="form-control" type="text" value="@Model.REPORT_ONDT" onblur="Calc_AF_ReportOnDate()" name="F_ReportOnDate" id="F_ReportOnDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.REPORT_TODT" onblur="Calc_AF_ReportToDate()" name="FBF_ReportToDate" id="FBF_ReportToDate" /></td>
                                    <td><input class="form-control" type="text" readonly value="@Model.BALANCE" onblur="Calc_AF_Balance()" name="F_Balance" id="F_Balance" /></td>
                                </tr>

                                  function SaveBFData() {
            debugger;
            var furnaces = ["C", "E", "F"];   
            var modelList = [];
            furnaces.forEach(function (f) {
                var model = {                    
                    FURNACE: f,
                    ACT_ONDT: Number($("#" + f + "_ActOnDate").val()) || 0,
                    REPORT_ONDT: Number($("#" + f + "_ReportOnDate").val()) || 0,
                    BALANCE: Number($("#" + f + "_Balance").val()) || 0
                };

                modelList.push(model);
            });

            $.ajax({
                url: '/HML/SaveBFProdData',  
                type: 'POST',
                data: JSON.stringify(modelList),
                contentType: 'application/json; charset=utf-8',
                dataType: 'json',

                success: function (res) {
                    if (res.success) {
                        alert("Saved Successfully");
                    } else {
                        alert("Error: " + res.message);
                    }
                },

                error: function () {
                    alert("Server error");
                }
            });
        }
         
        [HttpPost]
        public JsonResult SaveBFProdData(List<BF_Production> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    foreach (var model in modelList)
                    {
                        string query = @"
MERGE INTO TEST.T_BF_PRODUCTION_TRACKING t
USING (
    SELECT :FURNACE AS FURNACE,
           TO_DATE(:DATE_TIME,'DD/MM/YYYY') AS TIMESTAMP
    FROM dual
) s
ON (t.FURNACE = s.FURNACE AND t.TIMESTAMP = s.TIMESTAMP)

WHEN MATCHED THEN
    UPDATE SET 
        ACTUAL = :ACT,
        REPORTED = :RPT,
        BALANCE = :BAL

WHEN NOT MATCHED THEN
    INSERT (FURNACE, TIMESTAMP, ACTUAL, REPORTED, BALANCE)
    VALUES (:FURNACE, TO_DATE(:DATE_TIME,'DD/MM/YYYY'), :ACT, :RPT, :BAL)";

                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = model.FURNACE;
                            cmd.Parameters.Add("DATE_TIME", OracleDbType.Varchar2).Value = model.DATE_TIME;
                            cmd.Parameters.Add("ACT", OracleDbType.Decimal).Value = model.ACT_ONDT;
                            cmd.Parameters.Add("RPT", OracleDbType.Decimal).Value = model.REPORT_ONDT;
                            cmd.Parameters.Add("BAL", OracleDbType.Decimal).Value = model.BALANCE;
                            cmd.ExecuteNonQuery();
                        }
                    }
                }

                return Json(new { success = true });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
