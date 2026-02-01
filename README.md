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
            <script>
function SaveExceptionCast() {
    var furnace = $('#lstFur').val();

    var rows = document.querySelectorAll("#exception_cast tbody tr");
    var dataList = [];

    for (var i = 0; i < rows.length; i++) {
        var r = rows[i];

        // Grab values safely, even if empty
        var id = r.querySelector(".idno") ? r.querySelector(".idno").value : null;
        var tapholeNo = r.querySelector(".TapholeNo") ? r.querySelector(".TapholeNo").value : null;
        var date = r.querySelector(".ExceptionDate") ? r.querySelector(".ExceptionDate").value : null;
        var hh = r.querySelector(".hh") ? r.querySelector(".hh").value : null;
        var mm = r.querySelector(".mm") ? r.querySelector(".mm").value : null;
        var tapLen = r.querySelector(".TapholeLength") ? r.querySelector(".TapholeLength").value : null;
        var clay = r.querySelector(".Clay") ? r.querySelector(".Clay").value : null;
        var type = r.querySelector(".Type") ? r.querySelector(".Type").value : null;

        dataList[dataList.length] = {
            FURNACE: furnace || null,
            ID_NO: id,
            TAPHOLE_NO: tapholeNo,
            EXCEPTION_DATE: date,
            HH24: hh,
            MM: mm,
            TAPHOLE_LENGTH: tapLen,
            CLAY_PAUSED: clay,
            TYPE: type
        };
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
