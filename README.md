public JsonResult LoadOtherDetails()
{
    var data = new List<object>
    {
        new { CastNo = "1001", Date = "2025-07-20", Furnace = "Furnace A", MainRunnerHMAmt = 250.50, TiltingRunnerHMAmt = 130.75, Remarks = "OK" },
        new { CastNo = "1002", Date = "2025-07-19", Furnace = "Furnace B", MainRunnerHMAmt = 260.00, TiltingRunnerHMAmt = 140.25, Remarks = "Review" },
        new { CastNo = "1003", Date = "2025-07-18", Furnace = "Furnace C", MainRunnerHMAmt = 245.75, TiltingRunnerHMAmt = 125.50, Remarks = "Done" }
    };

    return Json(data, JsonRequestBehavior.AllowGet);
}
