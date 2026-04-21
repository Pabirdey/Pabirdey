[HttpPost]
public JsonResult RunProcedure(string p_date, string p_furnace)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            using (OracleCommand cmd = new OracleCommand("PROC_BF_PRODUCTION", con))
            {
                cmd.CommandType = CommandType.StoredProcedure;

                // INPUT PARAMETERS
                cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value =
                    DateTime.Parse(p_date);

                cmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value =
                    p_furnace;

                // OPTIONAL OUTPUT
                cmd.Parameters.Add("P_MSG", OracleDbType.Varchar2, 200)
                   .Direction = ParameterDirection.Output;

                cmd.ExecuteNonQuery();

                string msg = cmd.Parameters["P_MSG"].Value.ToString();

                return Json(new { status = true, message = msg });
            }
        }
    }
    catch (Exception ex)
    {
        return Json(new { status = false, message = ex.Message });
    }
}


<script>
    function runProcedure() {

        var date = $("#txtDate").val();

        // Furnace sequence
        var furnaces = ["C", "E", "F"];

        $("#msg").text("Processing...");

        // Loop one by one
        furnaces.forEach(function (furnace) {

            $.ajax({
                url: '/Home/RunProcedure',
                type: 'POST',
                data: {
                    p_date: date,
                    p_furnace: furnace
                },
                success: function (res) {
                    $("#msg").append("<br>" + furnace + " : " + res.message);
                },
                error: function () {
                    $("#msg").append("<br>" + furnace + " : Error");
                }
            });

        });
    }
</script>