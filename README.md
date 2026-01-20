using System.Collections.Generic;
using Oracle.ManagedDataAccess.Client;
using System.Web.Mvc;

[HttpPost]
public string SaveCarbonPaste(List<Dictionary<string, string>> list)
{
    OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString);
    con.Open();

    foreach (var row in list)
    {
        string DATE_TIME = row["DATE_TIME"];
        string SHIFT = row["SHIFT"];
        string BELOW_TUYERE = row["BELOW_TUYERE"];
        string NO_OF_DRUM = row["NO_OF_DRUM"];
        string FUR = row["FUR"];

        // 1️⃣ First try to UPDATE
        string updateSql = @"
            UPDATE TEST.T_FUR_CARBON_PASTE_INJECTION
            SET BELOW_TUYERE = :BELOW_TUYERE,
                NO_OF_DRUM = :NO_OF_DRUM
            WHERE TO_CHAR(DATE_TIME,'DD-MON-YYYY') = :DATE_TIME
              AND SHIFT = :SHIFT
              AND FUR_NAME = :FUR";

        OracleCommand upCmd = new OracleCommand(updateSql, con);

        upCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;

        upCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;

        upCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
        upCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;
        upCmd.Parameters.Add(":FUR", OracleDbType.Varchar2).Value = FUR;

        int rowsAffected = upCmd.ExecuteNonQuery();

        // 2️⃣ If no row updated → INSERT
        if (rowsAffected == 0)
        {
            string insertSql = @"
                INSERT INTO TEST.T_FUR_CARBON_PASTE_INJECTION
                (DATE_TIME, SHIFT, FUR_NAME, BELOW_TUYERE, NO_OF_DRUM)
                VALUES
                (TO_DATE(:DATE_TIME,'DD-MON-YYYY'),
                 :SHIFT, :FUR, :BELOW_TUYERE, :NO_OF_DRUM)";

            OracleCommand inCmd = new OracleCommand(insertSql, con);

            inCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
            inCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;
            inCmd.Parameters.Add(":FUR", OracleDbType.Varchar2).Value = FUR;
            inCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =
                string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;
            inCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =
                string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;

            inCmd.ExecuteNonQuery();
        }
    }

    con.Close();

    return "All rows inserted/updated successfully!";
}