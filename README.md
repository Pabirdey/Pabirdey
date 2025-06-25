[HttpPost]
public JsonResult Get_Fugitive_Violin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pPlantName)
{
    try
    {
        string sql = string.Empty;
        DataTable dt = new DataTable();
        Dictionary<string, object> param = new Dictionary<string, object>();

        if (pPlantName == "B10")
        {
            if (pBatteryNo == "10")
            {
                sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                      "FROM imtg.t_cp_fugitive_emission O " +
                      "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                      "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                      "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
            }
            else if (pBatteryNo == "11")
            {
                sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                      "FROM imtg.t_cp_fugitive_emission O " +
                      "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                      "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                      "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
            }
        }

        param.Add("pTimestamp", pTimestamp);
        param.Add("pOvenNo", pOvenNo);
        param.Add("pBatteryNo", pBatteryNo);

        dt = DAL.GetRecords(sql, param);
        return Json(dt, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        // Log error message (optional: write to file, database, etc.)
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}