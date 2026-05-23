   [HttpPost]
        public JsonResult SaveSignOff(string NAME,string SO_DATE,string SO_SHIFT,int SO_CHECK)
        {
            using (OracleConnection con =new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                OracleTransaction trans =con.BeginTransaction();
                try
                {
                    int VCOUNT = 0;                    

                    if (string.IsNullOrEmpty(NAME))
                    {
                        return Json(new
                        {
                            success = false,
                            message = "Select Your Name Please"
                        });
                    }
                    try
                    {
                        string authQuery = @"INSERT INTO DEMO.T_BF_SIGNOFF_AUTHORITY(NAME)VALUES(:NAME)";
                        OracleCommand authCmd =new OracleCommand(authQuery,con);
                        authCmd.Transaction = trans;
                        authCmd.Parameters.Add("NAME",OracleDbType.Varchar2).Value = NAME;
                        authCmd.ExecuteNonQuery();
                    }

                    catch (OracleException ex)
                    {                        
                        if (ex.Number != 1)
                        {
                            throw;
                        }
                    }
                    string countQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_SIGNOFF  WHERE SO_DATE =TO_DATE(:SO_DATE,'DD/MM/YYYY') AND SO_SHIFT = :SO_SHIFT  AND SO_PAGE = 'COKE_UNLOADING'";
                    OracleCommand countCmd =new OracleCommand(countQuery,con);
                    countCmd.Transaction = trans;
                    countCmd.Parameters.Add("SO_DATE",OracleDbType.Varchar2).Value = SO_DATE;
                    countCmd.Parameters.Add("SO_SHIFT",OracleDbType.Varchar2).Value = SO_SHIFT;
                    VCOUNT = Convert.ToInt32(countCmd.ExecuteScalar());                  
                    if (VCOUNT > 0)
                    {
                        string updateQuery = @"UPDATE DEMO.T_BF_SIGNOFF SET SO_CHECK=:SO_CHECK,NAME=:NAME,SO_TIME=SYSDATE  WHERE SO_DATE=TO_DATE(:SO_DATE,'DD/MM/YYYY') AND SO_SHIFT=:SO_SHIFT AND SO_PAGE='COKE_UNLOADING'";
                        OracleCommand updateCmd =new OracleCommand(updateQuery,con);
                        updateCmd.Transaction = trans;
                        updateCmd.Parameters.Add("SO_CHECK",OracleDbType.Int32).Value=SO_CHECK;
                        updateCmd.Parameters.Add("NAME",OracleDbType.Varchar2).Value=NAME;
                        updateCmd.Parameters.Add("SO_DATE",OracleDbType.Varchar2).Value=SO_DATE;
                        updateCmd.Parameters.Add("SO_SHIFT",OracleDbType.Varchar2).Value=SO_SHIFT;
                        updateCmd.ExecuteNonQuery();
                    }                   

                    else
                    {
                        string insertQuery = @"INSERT INTO DEMO.T_BF_SIGNOFF(NAME,SO_DATE,SO_SHIFT,SO_CHECK,SO_TIME,SO_PAGE)
                                            VALUES(:NAME,TO_DATE(:SO_DATE,'DD/MM/YYYY'),:SO_SHIFT,:SO_CHECK,SYSDATE,'COKE_UNLOADING')"; 

                        OracleCommand insertCmd =new OracleCommand(insertQuery,con);
                        insertCmd.Transaction = trans;
                        insertCmd.Parameters.Add("NAME",OracleDbType.Varchar2).Value = NAME;
                        insertCmd.Parameters.Add("SO_DATE",OracleDbType.Varchar2).Value = SO_DATE;
                        insertCmd.Parameters.Add("SO_SHIFT",OracleDbType.Varchar2).Value = SO_SHIFT;
                        insertCmd.Parameters.Add("SO_CHECK",OracleDbType.Int32).Value = SO_CHECK;
                        insertCmd.ExecuteNonQuery();
                    }
                    trans.Commit();                    
                    return Json(new
                    {
                        success=true,
                        SO_CHECK=SO_CHECK,
                        disableButton=SO_CHECK == 1 ? true : false
                    });
                }

                catch (Exception ex)
                {
                    trans.Rollback();

                    return Json(new
                    {
                        success = false,
                        message = ex.Message
                    });
                }
            }
        }
        function signoff() {   
    var obj = {
        NAME: $("#txtUser").val(),
        SO_DATE:lsSelectedFDate,
        SO_SHIFT:$("#ddlshift").val(),
        SO_CHECK:$("#signoff").is(":checked") ? 1 : 0
    };   

    $.ajax({
        url: '/Furnace_High_line/SaveSignOff',
        type: 'POST',
        data: obj,
        success: function (res) {
            if (res.success == true) {
                if (res.disableButton == true) {
                    $("#CokeUnloading").prop("disabled", true);                    
                }
                else {

                    $("#CokeUnloading").prop("disabled", false);
                   
                }                
            }
            else {
                alert(res.message);
            }

        },

        error: function () {

            alert("Error");

        }

    });

}
<script>
    function SaveCokeUnloading() {
        var SelectUser=$("#txtUser").val();
        var Signoff=$("#signoff").val();
        if(SelectUser=="" || SelectUser==null){
            alert("Please Select User Name");
            $("#txtUser").focus();
            return;
        }        
        $("#loaderDiv").show();
        var mainList = [];
        var cokeList = [];
        var nutList = [];    
        var mainRows = document.querySelectorAll("#tblBody tr");
        for (var i = 0; i < mainRows.length; i++) {
            var row = mainRows[i];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Shift: row.querySelector(".row-shift").value,
                Bunker: row.querySelector(".bunker").value,

                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,

                Total: row.querySelector(".total").value,
                Position: row.querySelector(".position").value,
                Balance: row.querySelector(".balance").value
            };

            mainList.push(obj);
        }    
        var cokeRows = document.querySelectorAll("#cokeTable tbody tr");
        for (var j = 0; j < cokeRows.length; j++) {
            var row = cokeRows[j];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            cokeList.push(obj);
        }

        var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }

        console.log("MAIN:", mainList);
        console.log("COKE:", cokeList);
        console.log("NUT:", nutList); 
        $.ajax({
            url: '/Furnace_High_line/SaveFurnaceCokeUnloading',
            type: 'POST',
            data: JSON.stringify({
                main: mainList,
                coke: cokeList,
                nut: nutList
            }),
            contentType: 'application/json',
            success: function (res) {               
                SaveFurnaceCokeUnloading_ID();
                signoff();
            },
            
            error: function (xhr) {
                $("#loaderDiv").hide();
                alert("Error : " + xhr.responseText);
            }
            
        });
    }

    function Furnace_Line_Coke_Unloading() {          
        var shift=$("#ddlshift").val();
        var furnaces = ["C", "E", "F"];
        $("#msg").text("Processing...");            
        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/Furnace_High_line/CallProcedure_Coke_Distribution',
                type: 'POST',
                data: {
                    p_date:lsSelectedFDate,
                    p_furnace: furnace,
                    P_shift:shift
                },
                success: function (res) {                   
                },
                error: function () {                    
                }
            });

        });
    }
</script>
