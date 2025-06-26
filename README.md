[HttpPost]
public JsonResult Get_Voilin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pPlantName)
{
    try
    {
        string sql = "";
        DataTable dt = new DataTable();
        Dictionary<string, object> param = new Dictionary<string, object>();

        if (pPlantName == "B10")
        {
            if (pBatteryNo == "10" || pBatteryNo == "11")
            {
                sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION, 2) AS PUSH_FORCE " +
                      "FROM imtg.t_cp_fugitive_emission O " +
                      "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                      "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                      "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";

                param.Add("pTimestamp", pTimestamp);
                param.Add("pOvenNo", pOvenNo);
                param.Add("pBatteryNo", pBatteryNo);

                dt = DAL.GetRecords(sql, param);
            }
        }

        return Json(dt, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        // 🔴 LOG or return the error message for debugging
        return Json(new { error = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}