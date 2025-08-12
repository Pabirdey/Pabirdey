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
                    SPLACING_WETNESS_TIME = :SPLACING_WETNESS_TIME,
                    CAST_TYPE = :CAST_TYPE,
                    CAST_CLAY_COND = :CAST_CLAY_COND,
                    TAPHOLE_BEHAVIOUR = :TAPHOLE_BEHAVIOUR,
                    HM_BEFORE_SLAG = :HM_BEFORE_SLAG,
                    HM_AFTER_SLAG = :HM_AFTER_SLAG,
                    HM_TEMP = :HM_TEMP,
                    DRILL_DIA = :DRILL_DIA,
                    DRILL_TYPE = :DRILL_TYPE,
                    DRILL_TIME = :DRILL_TIME,
                    NO_DRILL_BAR = :NO_DRILL_BAR,
                    NO_DRILL_BIT = :NO_DRILL_BIT,
                    NO_LANCING_PIPE = :NO_LANCING_PIPE,
                    NO_SHAFT_USED = :NO_SHAFT_USED,
                    DRILL_MC_AIR_PRESSURE = :DRILL_MC_AIR_PRESSURE,
                    TAPHOLE_LENGTH = :TAPHOLE_LENGTH,
                    LEN_DRILL_HAMMER = :LEN_DRILL_HAMMER,
                    COLOR_FUME_DRILLING = :COLOR_FUME_DRILLING,
                    SLAG_RETENTION = :SLAG_RETENTION,
                    SLAG_LADLE = :SLAG_LADLE,
                    NO_CINDER_GRANULATION = :NO_CINDER_GRANULATION,
                    GRANULATION_PERC = :GRANULATION_PERC,
                    CINDER_THEORETICAL_WT = :CINDER_THEORETICAL_WT,
                    SLAG_RATE = :SLAG_RATE,
                    TOTAL_SLAG = :TOTAL_SLAG
                WHERE CAST_NO = :CAST_NO 
                    AND DATE_TIME = TO_DATE(:Fdate, 'DD-MM-YYYY') 
                    AND FUR_NAME = :Fur";

            foreach (var row in data)
            {
                using (OracleCommand cmd = new OracleCommand(updateSql, conn))
                {
                    cmd.Parameters.Add(":CH_READY_TIME", StringOrDBNull(row, "CH_READY_TIME"));
                    cmd.Parameters.Add(":SPLACING_WETNESS_TIME", StringOrDBNull(row, "SPLACING_WETNESS_TIME"));
                    cmd.Parameters.Add(":CAST_TYPE", StringOrDBNull(row, "CAST_TYPE"));
                    cmd.Parameters.Add(":CAST_CLAY_COND", StringOrDBNull(row, "CAST_CLAY_COND"));
                    cmd.Parameters.Add(":TAPHOLE_BEHAVIOUR", StringOrDBNull(row, "TAPHOLE_BEHAVIOUR"));
                    cmd.Parameters.Add(":HM_BEFORE_SLAG", StringOrDBNull(row, "HM_BEFORE_SLAG"));
                    cmd.Parameters.Add(":HM_AFTER_SLAG", StringOrDBNull(row, "HM_AFTER_SLAG"));
                    cmd.Parameters.Add(":HM_TEMP", StringOrDBNull(row, "HM_TEMP"));
                    cmd.Parameters.Add(":DRILL_DIA", StringOrDBNull(row, "DRILL_DIA"));
                    cmd.Parameters.Add(":DRILL_TYPE", StringOrDBNull(row, "DRILL_TYPE"));
                    cmd.Parameters.Add(":DRILL_TIME", StringOrDBNull(row, "DRILL_TIME"));
                    cmd.Parameters.Add(":NO_DRILL_BAR", StringOrDBNull(row, "NO_DRILL_BAR"));
                    cmd.Parameters.Add(":NO_DRILL_BIT", StringOrDBNull(row, "NO_DRILL_BIT"));
                    cmd.Parameters.Add(":NO_LANCING_PIPE", StringOrDBNull(row, "NO_LANCING_PIPE"));
                    cmd.Parameters.Add(":NO_SHAFT_USED", StringOrDBNull(row, "NO_SHAFT_USED"));
                    cmd.Parameters.Add(":DRILL_MC_AIR_PRESSURE", StringOrDBNull(row, "DRILL_MC_AIR_PRESSURE"));
                    cmd.Parameters.Add(":TAPHOLE_LENGTH", StringOrDBNull(row, "TAPHOLE_LENGTH"));
                    cmd.Parameters.Add(":LEN_DRILL_HAMMER", StringOrDBNull(row, "LEN_DRILL_HAMMER"));
                    cmd.Parameters.Add(":COLOR_FUME_DRILLING", StringOrDBNull(row, "COLOR_FUME_DRILLING"));
                    cmd.Parameters.Add(":SLAG_RETENTION", StringOrDBNull(row, "SLAG_RETENTION"));
                    cmd.Parameters.Add(":SLAG_LADLE", StringOrDBNull(row, "SLAG_LADLE"));
                    cmd.Parameters.Add(":NO_CINDER_GRANULATION", StringOrDBNull(row, "NO_CINDER_GRANULATION"));
                    cmd.Parameters.Add(":GRANULATION_PERC", StringOrDBNull(row, "GRANULATION_PERC"));
                    cmd.Parameters.Add(":CINDER_THEORETICAL_WT", StringOrDBNull(row, "CINDER_THEORETICAL_WT"));
                    cmd.Parameters.Add(":SLAG_RATE", StringOrDBNull(row, "SLAG_RATE"));
                    cmd.Parameters.Add(":TOTAL_SLAG", StringOrDBNull(row, "TOTAL_SLAG"));
                    cmd.Parameters.Add(":CAST_NO", StringOrDBNull(row, "CAST_NO"));
                    cmd.Parameters.Add(":Fdate", Fdate);
                    cmd.Parameters.Add(":Fur", Fur);

                    cmd.ExecuteNonQuery();
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

private object StringOrDBNull(Dictionary<string, string> row, string key)
{
    if (!row.ContainsKey(key) || string.IsNullOrWhiteSpace(row[key]))
        return DBNull.Value;
    return row[key];
}
private object StringOrDBNull(Dictionary<string, string> row, string key)
{
    try
    {
        if (!row.ContainsKey(key))
            throw new ArgumentException($"Missing key: {key}");

        if (string.IsNullOrWhiteSpace(row[key]))
            return DBNull.Value;

        return row[key];
    }
    catch (Exception ex)
    {
        // Here you can log or directly throw a clear exception
        throw new Exception($"Error processing key '{key}': {ex.Message}");
    }
}