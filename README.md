public ActionResult Get_Display_Mudgun_Details(string Fdate, string Fur)
{
    var list = new[]
    {
        new { CAST_NO = 101, MG_CLAY_USED = "" },
        new { CAST_NO = 102, MG_CLAY_USED = "" }
    };

    return Json(Newtonsoft.Json.JsonConvert.SerializeObject(list),
                JsonRequestBehavior.AllowGet);
}
