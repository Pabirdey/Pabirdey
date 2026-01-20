[HttpPost]
public string SaveCarbonPaste(string DATE_TIME,
                              string SHIFT,
                              string BELOW_TUYERE,
                              string NO_OF_DRUM)
{
    OracleConnection con =
      new OracleConnection("User Id=xxx;Password=xxx;Data Source=xxx");

    con.Open();

    string updateSql = @"
    UPDATE CARBON_PASTE SET
        BELOW_TUYERE = :BELOW_TUYERE,
        NO_OF_DRUM = :NO_OF_DRUM
    WHERE DATE_TIME = :DATE_TIME
    AND SHIFT = :SHIFT";

    OracleCommand upCmd = new OracleCommand(updateSql, con);

    // ===== EXPLICIT TYPE BINDING =====
    upCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =
        string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;

    upCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =
        string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;

    upCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
    upCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;

    int rows = upCmd.ExecuteNonQuery();

    if (rows == 0)
    {
        string insertSql = @"
        INSERT INTO CARBON_PASTE
        (DATE_TIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM)
        VALUES
        (:DATE_TIME, :SHIFT, :BELOW_TUYERE, :NO_OF_DRUM)";

        OracleCommand inCmd = new OracleCommand(insertSql, con);

        inCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
        inCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;

        inCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;

        inCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;

        inCmd.ExecuteNonQuery();
    }

    con.Close();

    return "Saved Successfully";
}