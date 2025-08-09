[HttpPost]
public JsonResult SaveCastHouseData(List<Dictionary<string, string>> data, string Fdate, string Fur)
{
    try
    {
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            string updateSql = @"
                UPDATE TEST.T_CAST_DETAILS SET
                    CH_READY_TIME = :CH_READY_TIME,
                    SPLICING_WETNESS_TIME = :SPLICING_WETNESS_TIME,
                    CAST_TYPE = :CAST_TYPE,
                    CAST_CLAY_COND = :CAST_CLAY_COND,
                    TAPHOLE_BEHAVIOUR = :TAPHOLE_BEHAVIOUR,
                    HM_BEFORE_SLAG = :HM_BEFORE_SLAG,
                    HM_AFTER_SLAG = :HM_AFTER_SLAG,
                    HM_TEMP = :HM_TEMP
                WHERE CAST_NO = :CAST_NO
                  AND DATE_TIME = TO_DATE(:Fdate, 'DD-MM-YYYY')
                  AND FUR_NAME = :Fur";

            foreach (var row in data)
            {
                using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                {
                    updateCmd.Parameters.Add(":CH_READY_TIME", row["CH_READY_TIME"]);
                    updateCmd.Parameters.Add(":SPLICING_WETNESS_TIME", row["SPLICING_WETNESS_TIME"]);
                    updateCmd.Parameters.Add(":CAST_TYPE", row["CAST_TYPE"]);
                    updateCmd.Parameters.Add(":CAST_CLAY_COND", row["CAST_CLAY_COND"]);
                    updateCmd.Parameters.Add(":TAPHOLE_BEHAVIOUR", row["TAPHOLE_BEHAVIOUR"]);
                    updateCmd.Parameters.Add(":HM_BEFORE_SLAG", row["HM_BEFORE_SLAG"]);
                    updateCmd.Parameters.Add(":HM_AFTER_SLAG", row["HM_AFTER_SLAG"]);
                    updateCmd.Parameters.Add(":HM_TEMP", row["HM_TEMP"]);
                    updateCmd.Parameters.Add(":CAST_NO", row["CAST_NO"]);
                    updateCmd.Parameters.Add(":Fdate", Fdate);
                    updateCmd.Parameters.Add(":Fur", Fur);

                    updateCmd.ExecuteNonQuery();
                }
            }
        }

        return Json(new { success = true });
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message });
    }
}
