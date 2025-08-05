[HttpPost]
public JsonResult SaveData(List<Dictionary<string, string>> data)
{
    string connectionString = "your_connection_string";

    using (OracleConnection con = new OracleConnection(connectionString))
    {
        con.Open();

        foreach (var row in data)
        {
            using (OracleCommand cmd = new OracleCommand())
            {
                cmd.Connection = con;
                cmd.CommandText = @"INSERT INTO TAP_HOLE_TABLE
                (CAST_NO, TROUGH_NO, CAST_ST_TIME, CAST_END_TIME, CAST_CLAY_COND)
                VALUES (:CAST_NO, :TROUGH_NO, :CAST_ST_TIME, :CAST_END_TIME, :CAST_CLAY_COND)";

                cmd.Parameters.Add(":CAST_NO", row["CAST_NO"]);
                cmd.Parameters.Add(":TROUGH_NO", row["TROUGH_NO"]);
                cmd.Parameters.Add(":CAST_ST_TIME", row["CAST_ST_TIME"]);
                cmd.Parameters.Add(":CAST_END_TIME", row["CAST_END_TIME"]);
                cmd.Parameters.Add(":CAST_CLAY_COND", row["CAST_CLAY_COND"]);

                cmd.ExecuteNonQuery();
            }
        }
    }

    return Json("OK");
}
