public class ProductionController : Controller
{
    private readonly string conString =
        ConfigurationManager.ConnectionStrings["OracleDb"].ConnectionString;

    [HttpGet]
    public JsonResult Index(DateTime prodDate)
    {
        BlastFurnaceViewModel model = new BlastFurnaceViewModel();

        try
        {
            model.ControlDateTimeProd = prodDate;

            using (OracleConnection con = new OracleConnection(conString))
            {
                con.Open();

                int vTemp = 0;

                string countQuery = @"
                    SELECT COUNT(*)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP = :prodDate
                    AND FURNACE IN ('C','D','E','F')";

                using (OracleCommand cmd = new OracleCommand(countQuery, con))
                {
                    cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = prodDate;

                    vTemp = Convert.ToInt32(cmd.ExecuteScalar());
                }

                // If record exists in production tracking table
                if (vTemp > 0)
                {
                    LoadFurnaceData(con, prodDate, "C", model);
                    LoadFurnaceData(con, prodDate, "D", model);
                    LoadFurnaceData(con, prodDate, "E", model);
                    LoadFurnaceData(con, prodDate, "F", model);
                }
                else
                {
                    // Load from ladle details table
                    LoadActualFromLadle(con, prodDate, "C", model);
                    LoadActualFromLadle(con, prodDate, "D", model);
                    LoadActualFromLadle(con, prodDate, "E", model);
                    LoadActualFromLadle(con, prodDate, "F", model);
                }

                // Load Summary
                LoadLadleSummary(con, prodDate, model);

                // Total Actual
                model.DisplayActual =
                    (model.ActualC ?? 0) +
                    (model.ActualD ?? 0) +
                    (model.ActualE ?? 0) +
                    (model.ActualF ?? 0);

                // Total Reported
                model.DisplayReported =
                    (model.ReportedC ?? 0) +
                    (model.ReportedD ?? 0) +
                    (model.ReportedE ?? 0) +
                    (model.ReportedF ?? 0);

                // Total Balance
                model.DisplayBalance =
                    (model.BalanceC ?? 0) +
                    (model.BalanceD ?? 0) +
                    (model.BalanceE ?? 0) +
                    (model.BalanceF ?? 0);
            }

            // Success Response
            return Json(new
            {
                success = true,
                message = "Data loaded successfully.",
                data = model
            }, JsonRequestBehavior.AllowGet);
        }
        catch (OracleException ex)
        {
            // Oracle DB Exception
            return Json(new
            {
                success = false,
                message = "Oracle database error occurred.",
                error = ex.Message
            }, JsonRequestBehavior.AllowGet);
        }
        catch (Exception ex)
        {
            // General Exception
            return Json(new
            {
                success = false,
                message = "Unexpected error occurred.",
                error = ex.Message
            }, JsonRequestBehavior.AllowGet);
        }
        finally
        {
            // Optional cleanup or logging
        }
    }
}
