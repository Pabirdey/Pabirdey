[HttpPost]
public JsonResult SaveSignOff(
    string NAME,
    string SO_DATE,
    string SO_SHIFT,
    int SO_CHECK)
{
    using (OracleConnection con =
        new OracleConnection(
            iMonitorWebUtils.msConRWString))
    {
        con.Open();

        OracleTransaction trans =
            con.BeginTransaction();

        try
        {
            int VCOUNT = 0;

            // ============================
            // NAME VALIDATION
            // ============================

            if (string.IsNullOrEmpty(NAME))
            {
                return Json(new
                {
                    success = false,
                    message = "Select Your Name Please"
                });
            }

            // ============================
            // INSERT AUTHORITY TABLE
            // ============================

            try
            {
                string authQuery = @"
                    INSERT INTO
                    DEMO.T_BF_SIGNOFF_AUTHORITY
                    (
                        NAME
                    )
                    VALUES
                    (
                        :NAME
                    )";

                OracleCommand authCmd =
                    new OracleCommand(
                        authQuery,
                        con);

                authCmd.Transaction = trans;

                authCmd.Parameters.Add(
                    "NAME",
                    OracleDbType.Varchar2)
                    .Value = NAME;

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

            // ============================
            // CHECK COUNT
            // ============================

            string countQuery = @"
                SELECT COUNT(*)
                FROM DEMO.T_BF_SIGNOFF
                WHERE SO_DATE =
                TO_DATE(:SO_DATE,'YYYY-MM-DD')
                AND SO_SHIFT = :SO_SHIFT
                AND SO_PAGE = 'COKE_UNLOADING'";

            OracleCommand countCmd =
                new OracleCommand(
                    countQuery,
                    con);

            countCmd.Transaction = trans;

            countCmd.Parameters.Add(
                "SO_DATE",
                OracleDbType.Varchar2)
                .Value = SO_DATE;

            countCmd.Parameters.Add(
                "SO_SHIFT",
                OracleDbType.Varchar2)
                .Value = SO_SHIFT;

            VCOUNT = Convert.ToInt32(
                countCmd.ExecuteScalar());

            // ============================
            // UPDATE
            // ============================

            if (VCOUNT > 0)
            {
                string updateQuery = @"
                    UPDATE DEMO.T_BF_SIGNOFF
                    SET SO_CHECK = :SO_CHECK,
                        NAME     = :NAME,
                        SO_TIME  = SYSDATE
                    WHERE SO_DATE =
                    TO_DATE(:SO_DATE,'YYYY-MM-DD')
                    AND SO_SHIFT = :SO_SHIFT
                    AND SO_PAGE = 'COKE_UNLOADING'";

                OracleCommand updateCmd =
                    new OracleCommand(
                        updateQuery,
                        con);

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
                        TO_DATE(:SO_DATE,'YYYY-MM-DD'),
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
function signoff() {

    var obj = {

        NAME: $("#txtUser").val(),

        SO_DATE: $("#currDate-value").val(),

        SO_SHIFT: $("#ddlshift").val(),

        SO_CHECK:
            $("#signoff").is(":checked") ? 1 : 0
    };

    $.ajax({

        url: '/Furnace_High_line/SaveSignOff',

        type: 'POST',

        data: obj,

        success: function (res) {

            if (res.success == true) {

                if (res.disableButton == true) {

                    $("#PBSAVE")
                        .prop("disabled", true);

                    $("#PBDELETE")
                        .prop("disabled", true);
                }
                else {

                    $("#PBSAVE")
                        .prop("disabled", false);

                    $("#PBDELETE")
                        .prop("disabled", false);
                }

                alert("Saved Successfully");
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
