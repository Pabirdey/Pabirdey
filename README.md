[HttpPost]
public JsonResult Get_CP_Fugitivity_Voilin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pSCP, string pPlantName)
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
            param.Add("pBatteryNo", pBatteryNo); // fixed key

            dt = DAL.GetRecords(sql, param);
        }
    }

    return Json(dt, JsonRequestBehavior.AllowGet); // Directly return DataTable as JSON
}