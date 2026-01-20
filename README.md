[HttpPost]
public string Save_Carbon_Paste(string jsonData)
{
    try
    {
        JArray arr = JArray.Parse(jsonData);

        OracleConnection con =
          new OracleConnection("User Id=xxx;Password=xxx;Data Source=xxx");

        con.Open();

        foreach (var item in arr)
        {
            string sql = @"
MERGE INTO T_CARBON_PASTE t
USING dual
ON (t.DATE_TIME = TO_DATE(:DATE_TIME,'YYYY-MM-DD HH24:MI:SS')
    AND t.SHIFT = :SHIFT)

WHEN MATCHED THEN
  UPDATE SET
     BELOW_TUYERE = :BELOW_TUYERE,
     NO_OF_DRUM   = :NO_OF_DRUM

WHEN NOT MATCHED THEN
  INSERT
  (DATE_TIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM)
  VALUES
  (TO_DATE(:DATE_TIME,'YYYY-MM-DD HH24:MI:SS'),
   :SHIFT, :BELOW_TUYERE, :NO_OF_DRUM)";

            OracleCommand cmd =
                new OracleCommand(sql, con);

            cmd.Parameters.Add(":DATE_TIME",
                item["DATE_TIME"].ToString());

            cmd.Parameters.Add(":SHIFT",
                item["SHIFT"].ToString());

            cmd.Parameters.Add(":BELOW_TUYERE",
                item["BELOW_TUYERE"].ToString());

            cmd.Parameters.Add(":NO_OF_DRUM",
                item["NO_OF_DRUM"].ToString());

            cmd.ExecuteNonQuery();
        }

        con.Close();

        return "Data Saved Successfully";
    }
    catch (Exception ex)
    {
        return ex.Message;
    }
}