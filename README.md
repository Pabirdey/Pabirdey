private decimal GetGrossWt(string trpNo, DateTime date, DateTime time)
{
    decimal grossWt = 0;

    string conStr = ConfigurationManager.ConnectionStrings["OracleDbContext"].ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        string sql = @"
            SELECT NVL(GROSS_WT,0)
            FROM Demo.T_LADLE_DETAILS
            WHERE TRP_NO = :TRP_NO
            AND LADLE_FLEND_TIME =
            (
                SELECT MAX(LADLE_FLEND_TIME)
                FROM Demo.T_LADLE_DETAILS
                WHERE TRP_NO = :TRP_NO
                AND LADLE_FLEND_TIME <= :END_TIME
            )";

        using (OracleCommand cmd = new OracleCommand(sql, con))
        {
            cmd.Parameters.Add("TRP_NO", OracleDbType.Varchar2).Value = trpNo;

            DateTime endDateTime = date.Date.Add(time.TimeOfDay);

            cmd.Parameters.Add("END_TIME", OracleDbType.Date).Value = endDateTime;

            object result = cmd.ExecuteScalar();

            if (result != null && result != DBNull.Value)
            {
                grossWt = Convert.ToDecimal(result);
            }
        }
    }

    return grossWt;
}
