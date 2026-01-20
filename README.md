[HttpPost]
public string SaveCarbonPaste(string DATE_TIME,
                              string SHIFT,
                              string BELOW_TUYERE,
                              string NO_OF_DRUM)
{
    OracleConnection con =
      new OracleConnection("User Id=xxx;Password=xxx;Data Source=xxx");

    con.Open();

    // ----- FIRST UPDATE -----
    string updateSql = @"
    UPDATE CARBON_PASTE SET
        BELOW_TUYERE = :BELOW_TUYERE,
        NO_OF_DRUM = :NO_OF_DRUM
    WHERE DATE_TIME = :DATE_TIME
    AND SHIFT = :SHIFT";

    OracleCommand upCmd = new OracleCommand(updateSql, con);

    upCmd.Parameters.Add(":BELOW_TUYERE", BELOW_TUYERE);
    upCmd.Parameters.Add(":NO_OF_DRUM", NO_OF_DRUM);
    upCmd.Parameters.Add(":DATE_TIME", DATE_TIME);
    upCmd.Parameters.Add(":SHIFT", SHIFT);

    int rows = upCmd.ExecuteNonQuery();

    // ----- IF NOT UPDATED → INSERT -----
    if (rows == 0)
    {
        string insertSql = @"
        INSERT INTO CARBON_PASTE
        (DATE_TIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM)
        VALUES
        (:DATE_TIME, :SHIFT, :BELOW_TUYERE, :NO_OF_DRUM)";

        OracleCommand inCmd = new OracleCommand(insertSql, con);

        inCmd.Parameters.Add(":DATE_TIME", DATE_TIME);
        inCmd.Parameters.Add(":SHIFT", SHIFT);
        inCmd.Parameters.Add(":BELOW_TUYERE", BELOW_TUYERE);
        inCmd.Parameters.Add(":NO_OF_DRUM", NO_OF_DRUM);

        inCmd.ExecuteNonQuery();
    }

    con.Close();

    return "Saved Successfully";
}