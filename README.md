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
                        // DUP_VAL_ON_INDEX
                        if (ex.Number != 1)
                        {
                            throw;
                        }
                    }
                    string countQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_SIGNOFF  WHERE SO_DATE =TO_DATE(:SO_DATE,'DD/MM/YYYY'') AND SO_SHIFT = :SO_SHIFT  AND SO_PAGE = 'COKE_UNLOADING'";
                    OracleCommand countCmd =new OracleCommand(countQuery,con);
                    countCmd.Transaction = trans;
                    countCmd.Parameters.Add("SO_DATE",OracleDbType.Varchar2).Value = SO_DATE;
                    countCmd.Parameters.Add("SO_SHIFT",OracleDbType.Varchar2).Value = SO_SHIFT;
                    VCOUNT = Convert.ToInt32(countCmd.ExecuteScalar());                  
                    if (VCOUNT > 0)
                    {
                        string updateQuery = @"UPDATE DEMO.T_BF_SIGNOFF SET SO_CHECK=:SO_CHECK,NAME=:NAME,SO_TIME=SYSDATE  WHERE SO_DATE=TO_DATE(:SO_DATE,'DD/MM/YYYY'') AND SO_SHIFT=:SO_SHIFT AND SO_PAGE='COKE_UNLOADING'";
                        OracleCommand updateCmd =new OracleCommand(updateQuery,con);
                        updateCmd.Transaction = trans;

                        updateCmd.Parameters.Add(
                            "SO_CHECK",
                            OracleDbType.Int32)
                            .Value = SO_CHECK;

                        updateCmd.Parameters.Add(
                            "NAME",
                            OracleDbType.Varchar2)
                            .Value = NAME;

                        updateCmd.Parameters.Add(
                            "SO_DATE",
                            OracleDbType.Varchar2)
                            .Value = SO_DATE;

                        updateCmd.Parameters.Add(
                            "SO_SHIFT",
                            OracleDbType.Varchar2)
                            .Value = SO_SHIFT;

                        updateCmd.ExecuteNonQuery();
                    }

                    // ============================
                    // INSERT
                    // ============================

                    else
                    {
                        string insertQuery = @"
                    INSERT INTO DEMO.T_BF_SIGNOFF
                    (
                        NAME,
                        SO_DATE,
                        SO_SHIFT,
                        SO_CHECK,
                        SO_TIME,
                        SO_PAGE
                    )
                    VALUES
                    (
                        :NAME,
                        TO_DATE(:SO_DATE,'DD/MM/YYYY''),
                        :SO_SHIFT,
                        :SO_CHECK,
                        SYSDATE,
                        'COKE_UNLOADING'
                    )";

                        OracleCommand insertCmd =
                            new OracleCommand(
                                insertQuery,
                                con);

                        insertCmd.Transaction = trans;

                        insertCmd.Parameters.Add(
                            "NAME",
                            OracleDbType.Varchar2)
                            .Value = NAME;

                        insertCmd.Parameters.Add(
                            "SO_DATE",
                            OracleDbType.Varchar2)
                            .Value = SO_DATE;

                        insertCmd.Parameters.Add(
                            "SO_SHIFT",
                            OracleDbType.Varchar2)
                            .Value = SO_SHIFT;

                        insertCmd.Parameters.Add(
                            "SO_CHECK",
                            OracleDbType.Int32)
                            .Value = SO_CHECK;

                        insertCmd.ExecuteNonQuery();
                    }

                    trans.Commit();

                    // ============================
                    // RETURN RESULT
                    // ============================

                    return Json(new
                    {
                        success = true,
                        SO_CHECK = SO_CHECK,
                        disableButton =
                            SO_CHECK == 1 ? true : false
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


