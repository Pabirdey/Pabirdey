[HttpPost]
public string Save_Carbon_Paste(
      string DATE_TIME,
      string SHIFT,
      string BELOW_TUYERE,
      string NO_OF_DRUM)
{
    OracleConnection con =
      new OracleConnection("User Id=xxx;Password=xxx;Data Source=xxx");

    try
    {
        con.Open();

        string sql = @"
MERGE INTO T_CARBON_PASTE t
USING dual
ON (t.DATE_TIME =
      TO_DATE(:DATE_TIME,'YYYY-MM-DD HH24:MI:SS')
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

        cmd.Parameters.Add(":DATE_TIME", DATE_TIME);
        cmd.Parameters.Add(":SHIFT", SHIFT);
        cmd.Parameters.Add(":BELOW_TUYERE", BELOW_TUYERE);
        cmd.Parameters.Add(":NO_OF_DRUM", NO_OF_DRUM);

        cmd.ExecuteNonQuery();

        return "OK";
    }
    catch (Exception ex)
    {
        return ex.Message;
    }
    finally
    {
        con.Close();
    }
}