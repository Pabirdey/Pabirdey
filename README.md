[HttpPost]
public JsonResult SaveData(List<GranshotModel> model)
{
    using (OracleConnection con =
           new OracleConnection(conStr))
    {
        con.Open();

        foreach (var item in model)
        {
            OracleCommand cmd = new OracleCommand();

            cmd.Connection = con;

            cmd.CommandText = @"INSERT INTO T_GRANSHOT
                                (
                                  CAST_NO,
                                  CAST_START_DT,
                                  CAST_END_DT,
                                  LADLE_NO,
                                  LADLE_START_DT,
                                  LADLE_END_DT,
                                  ARRIVED_FROM,
                                  GROSS,
                                  TARE,
                                  NET
                                )
                                VALUES
                                (
                                  :CAST_NO,
                                  :CAST_START_DT,
                                  :CAST_END_DT,
                                  :LADLE_NO,
                                  :LADLE_START_DT,
                                  :LADLE_END_DT,
                                  :ARRIVED_FROM,
                                  :GROSS,
                                  :TARE,
                                  :NET
                                )";

            cmd.Parameters.Add(":CAST_NO", item.CAST_NO);
            cmd.Parameters.Add(":CAST_START_DT", item.CAST_START_DT);
            cmd.Parameters.Add(":CAST_END_DT", item.CAST_END_DT);
            cmd.Parameters.Add(":LADLE_NO", item.LADLE_NO);
            cmd.Parameters.Add(":LADLE_START_DT", item.LADLE_START_DT);
            cmd.Parameters.Add(":LADLE_END_DT", item.LADLE_END_DT);
            cmd.Parameters.Add(":ARRIVED_FROM", item.ARRIVED_FROM);
            cmd.Parameters.Add(":GROSS", item.GROSS);
            cmd.Parameters.Add(":TARE", item.TARE);
            cmd.Parameters.Add(":NET", item.NET);

            cmd.ExecuteNonQuery();
        }
    }

    return Json(new { success = true });
}