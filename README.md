 <script>
        function SaveExceptionCast() {
            debugger;
            var furnace =$('#lstFur').val();
        var rows = document.querySelectorAll("#exception_cast tbody tr"); 
        var dataList = [];
    for (var i = 0; i < rows.length; i++) {
    var r = rows[i];
        dataList.push({
        FURNACE: furnace,
        ID_NO: r.querySelector(".idno").value,
        TAPHOLE_NO: r.querySelector(".TapholeNo").value,
        EXCEPTION_DATE: r.querySelector(".ExceptionDate").value,
        HH24: r.querySelector(".hh").value,
        MM: r.querySelector(".mm").value,
        TAPHOLE_LENGTH: r.querySelector(".TapholeLength").value,
        CLAY_PAUSED: r.querySelector(".Clay").value,
        TYPE: r.querySelector(".Type").value
        });
    }
    $.ajax({
        url: "/CastHouse/Save_Exception_Cast",
        type: "POST",
        data: JSON.stringify(dataList),
        contentType: "application/json",
        success: function (res) {
        alert(res);
        },
        error: function () {
        alert("Error while saving");
        }
    });
    }
    </script>
    function addRow() {
    var tr = "<tr>";

    tr += "<td><input name='ID_NO' class='form-control form-control-md idno' autocomplete='off' onclick='generateId(this)'></td>";
    tr += "<td><select name='TAPHOLE_NO' class='form-select form-select-md TapholeNO'><option></option><option>1</option><option>2</option><option>3</option><option>4</option></select></td>";
    tr += "<td><input name='DATE_TIME' class='form-control form-control-md' autocomplete='off' onclick='setDeclaredDate(this)'></td>";

    tr += "<td><select name='HH' class='form-select form-select-md'><option></option>";
    for (var h = 0; h < 24; h++) tr += "<option>" + (h < 10 ? "0" : "") + h + "</option>";
    tr += "</select></td>";

    tr += "<td><select name='MM' class='form-select form-select-md'><option></option>";
    for (var m = 0; m <= 55; m += 5) tr += "<option>" + (m < 10 ? "0" : "") + m + "</option>";
    tr += "</select></td>";

    tr += "<td><input name='TAPHOLE_LENGTH' class='form-control form-control-md' autocomplete='off'></td>";
    tr += "<td><input name='CLAY_PUSHED' class='form-control form-control-md' autocomplete='off'></td>";

    tr += "<td><select name='TYPE' class='form-select form-select-md'><option></option>";
    tr += "<option>BLEEDING HOLE</option><option>HOLE THROUGH</option><option>BLANK PUSH</option></select></td>";

    tr += "</tr>";

    $("#exception_cast tbody").append(tr);
}
    <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="SaveExceptionCast()">
                                    <b>Save</b>
                                </button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
                                <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
                                    <thead class="table-secondary sticky-top">
                                        <tr>
                                            <th class="idno" style="width:150px;">ID No</th>
                                            <th class="TapholeNO" style="width:50px;">TAPHOLE No</th>
                                            <th class="ExceptionDate" style="width:180px;">Date</th>
                                            <th class="hh" style="width:90px;">HH24</th>
                                            <th class="mm"style="width:90px;">MM</th>
                                            <th class="TapholeLength">Taphole Length</th>
                                            <th class="ClayPaused">Clay Paused</th>
                                            <th class="Type" style="width:240px;">Type</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <!-- rows created by JS -->
                                    </tbody>
                                </table>
                            </div>
                              [HttpPost]
        public JsonResult Save_Exception_Cast(List<dynamic> data)
        {
            using (OracleConnection con =new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                for (int i = 0; i < data.Count; i++)                {
                    string idNo = Convert.ToString(data[i].ID_NO);
                    string tapholeno = Convert.ToString(data[i].TAPHOLE_NO);
                    string furnace = Convert.ToString(data[i].FURNACE);
                    string exceptiondate = Convert.ToString(data[i].EXCEPTION_DATE);
                    string hh24 = Convert.ToString(data[i].HH24);
                    string mm = Convert.ToString(data[i].MM);
                    string tapholelength = Convert.ToString(data[i].TAPHOLE_LENGTH);
                    string claypaused = Convert.ToString(data[i].CLAY_PAUSED);
                    string type = Convert.ToString(data[i].TYPE);
                    
                    if (string.IsNullOrEmpty(idNo) && string.IsNullOrEmpty(exceptiondate))
                    {
                        continue;
                    }                    
                    string chkSql = @"SELECT COUNT(1) FROM Test.T_CAST_EXCEPTION WHERE DATE_TIME=:P_DATE AND ID_NO=:P_ID AND FURNACE=:P_FURNACE";
                    OracleCommand chkCmd = new OracleCommand(chkSql, con);
                    chkCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                    chkCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptiondate;
                    chkCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                    int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());
                    if (cnt > 0)
                    {                       
                        string updSql = @"UPDATE Test.T_CAST_EXCEPTION SET CAST_DATE =TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,'DD/MM/YYYY HH24:MI'),HH24=:P_HH,MM=:P_MM WHERE ID_NO=:P_ID AND FURNACE=:P_FURNACE";
                        OracleCommand updCmd = new OracleCommand(updSql, con);
                        updCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptiondate;
                        updCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                        updCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                        updCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                        updCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = claypaused;
                        updCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type;
                        updCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeno;
                        updCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapholelength;
                        updCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                        updCmd.ExecuteNonQuery();
                    }
                    else
                    {                        
                        string insSql = @"INSERT INTO Test.T_CAST_EXCEPTION(DATE_TIME,FUR_NAME,ID_NO,TAPHOLE_LENGTH,CLAY_PUSHED,TYPE,TAPHOLE_NO)VALUES(TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,'DD/MM/YYYY HH24:MI'),:P_HH,:P_MM),:P_FURNACE,:P_ID,:P_TAPHOLELENGTH,:P_CLAY,:P_TYPE,:P_TAPHOLENO)";
                        OracleCommand insCmd = new OracleCommand(insSql, con);
                        insCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                        insCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptiondate;
                        insCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                        insCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                        insCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                        insCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = claypaused;
                        insCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type;
                        insCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeno;
                        insCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapholelength;
                        insCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                        insCmd.ExecuteNonQuery();
                    }
                }
            }

            return Json("Insert / Update completed successfully");
        }
