public class CastHouseController : Controller
{
    public ActionResult Index()
    {
        return View();
    }

    [HttpGet]
    public JsonResult LoadCastData()
    {
        var data = new[]
        {
            new { CastNo = 1, TroughNo = "T1", CastStart = "10:00", Duration = "1.5", Rate = "2.0", TLC = "A", OT = "OT1", Ready = "10:15", Wetness = "10:20", CastType = "Normal", Clay = "Good", Taphole = "Normal" },
            new { CastNo = 2, TroughNo = "T2", CastStart = "11:00", Duration = "1.4", Rate = "2.2", TLC = "B", OT = "OT2", Ready = "11:15", Wetness = "11:25", CastType = "Emergency", Clay = "Soft", Taphole = "Leakage" },
            // Add more if needed
        };

        return Json(data, JsonRequestBehavior.AllowGet);
    }
}