[HttpPost]
public JsonResult SaveSignOff(SignOffModel model)
{
    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        OracleTransaction trans = con.BeginTransaction();

        try
        {
            int vCount = 0;

            // =========================
            // CHECK RECORD EXISTS
            // =========================

            string checkQuery = @"
                SELECT COUNT(*)
                FROM DEMO.T_BF_SIGNOFF
                WHERE SO_DATE  = :SO_DATE
                AND   SO_SHIFT = :SO_SHIFT
                AND   SO_PAGE  = 'COKE_UNLOADING'";

            OracleCommand checkCmd =
                new OracleCommand(checkQuery, con);

            checkCmd.Transaction = trans;

            checkCmd.Parameters.Add("SO_DATE",
                OracleDbType.Date).Value = model.SO_DATE;

            checkCmd.Parameters.Add("SO_SHIFT",
                OracleDbType.Varchar2).Value = model.SO_SHIFT;

            vCount = Convert.ToInt32(checkCmd.ExecuteScalar());

            // =========================
            // UPDATE
            // =========================

            if (vCount > 0)
            {
                string updateQuery = @"
                    UPDATE DEMO.T_BF_SIGNOFF
                    SET SO_CHECK = :SO_CHECK,
                        NAME     = :NAME,
                        SO_TIME  = SYSDATE
                    WHERE SO_DATE  = :SO_DATE
                    AND   SO_SHIFT = :SO_SHIFT
                    AND   SO_PAGE  = 'COKE_UNLOADING'";

                OracleCommand updateCmd =
                    new OracleCommand(updateQuery, con);

                updateCmd.Transaction = trans;

                updateCmd.Parameters.Add("SO_CHECK",
                    OracleDbType.Int32).Value = model.SO_CHECK;

                updateCmd.Parameters.Add("NAME",
                    OracleDbType.Varchar2).Value = model.NAME;

                updateCmd.Parameters.Add("SO_DATE",
                    OracleDbType.Date).Value = model.SO_DATE;

                updateCmd.Parameters.Add("SO_SHIFT",
                    OracleDbType.Varchar2).Value = model.SO_SHIFT;

                updateCmd.ExecuteNonQuery();
            }

            // =========================
            // INSERT
            // =========================

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
                        :SO_DATE,
                        :SO_SHIFT,
                        :SO_CHECK,
                        SYSDATE,
                        'COKE_UNLOADING'
                    )";

                OracleCommand insertCmd =
                    new OracleCommand(insertQuery, con);

                insertCmd.Transaction = trans;

                insertCmd.Parameters.Add("NAME",
                    OracleDbType.Varchar2).Value = model.NAME;

                insertCmd.Parameters.Add("SO_DATE",
                    OracleDbType.Date).Value = model.SO_DATE;

                insertCmd.Parameters.Add("SO_SHIFT",
                    OracleDbType.Varchar2).Value = model.SO_SHIFT;

                insertCmd.Parameters.Add("SO_CHECK",
                    OracleDbType.Int32).Value = model.SO_CHECK;

                insertCmd.ExecuteNonQuery();
            }

            trans.Commit();

            return Json(new
            {
                success = true,
                message = "Saved Successfully"
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

public class SignOffModel
{
    public string NAME { get; set; }

    public DateTime SO_DATE { get; set; }

    public string SO_SHIFT { get; set; }

    public int SO_CHECK { get; set; }
}
function SaveSignOff() {

    var obj = {

        NAME: $("#txtUser").val(),

        SO_DATE: $("#txtDate").val(),

        SO_SHIFT: $("#ddlShift").val(),

        SO_CHECK: $("#signoff").is(":checked") ? 1 : 0
    };

    $.ajax({

        url: '/Furnace_High_line/SaveSignOff',

        type: 'POST',

        data: obj,

        success: function (res) {

            alert(res.message);

            // Disable Button
            if (obj.SO_CHECK == 1) {

                $("#PBSAVE").prop("disabled", true);

                $("#PBDELETE").prop("disabled", true);
            }
            else {

                $("#PBSAVE").prop("disabled", false);

                $("#PBDELETE").prop("disabled", false);
            }

        },

        error: function () {

            alert("Error");

        }

    });

}
