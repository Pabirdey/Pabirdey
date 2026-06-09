private decimal GetHmt(string trpNo, DateTime date, DateTime time, string from)
{
    decimal hmt = 0;

    string constr = ConfigurationManager.ConnectionStrings["OracleDbContext"].ConnectionString;

    using (OracleConnection con = new OracleConnection(constr))
    {
        con.Open();

        string sql = @"
            SELECT NVL(HMT,0)
            FROM Demo.T_LADLE_DETAILS
            WHERE FUR_NAME = :FUR_NAME
              AND TRP_NO = :TRP_NO
              AND LADLE_FLEND_TIME =
              (
                  SELECT MAX(LADLE_FLEND_TIME)
                  FROM Demo.T_LADLE_DETAILS
                  WHERE FUR_NAME = :FUR_NAME
                    AND TRP_NO = :TRP_NO
                    AND HMT IS NOT NULL
                    AND LADLE_FLEND_TIME <= :END_TIME
              )";

        using (OracleCommand cmd = new OracleCommand(sql, con))
        {
            cmd.Parameters.Add("FUR_NAME", OracleDbType.Varchar2).Value = from;
            cmd.Parameters.Add("TRP_NO", OracleDbType.Varchar2).Value = trpNo;

            DateTime endDateTime = date.Date.Add(time.TimeOfDay);

            cmd.Parameters.Add("END_TIME", OracleDbType.Date).Value = endDateTime;

            object result = cmd.ExecuteScalar();

            if (result != null && result != DBNull.Value)
            {
                hmt = Convert.ToDecimal(result);
            }
        }
    }

    return hmt;
}
