private void LoadActualFromLadle(
    OracleConnection con,
    DateTime prodDate,
    string furnace,
    BlastFurnaceViewModel model)
{
    string query = @"
        SELECT SUM(NET_WT)
        FROM DEMO.T_LADLE_DETAILS
        WHERE LADLE_FLEND_TIME >= :fromDate
        AND LADLE_FLEND_TIME < :toDate
        AND DESTINATION <> 'R'
        AND FUR_NAME = :furnace";

    decimal actual = 0;

    using (OracleCommand cmd = new OracleCommand(query, con))
    {
        cmd.Parameters.Add("fromDate", OracleDbType.Date)
            .Value = prodDate.AddHours(6);

        cmd.Parameters.Add("toDate", OracleDbType.Date)
            .Value = prodDate.AddDays(1).AddHours(6);

        cmd.Parameters.Add("furnace", OracleDbType.Varchar2)
            .Value = furnace;

        object result = cmd.ExecuteScalar();

        actual = result == DBNull.Value ? 0 : Convert.ToDecimal(result);
    }

    switch (furnace)
    {
        case "C":
            model.ActualC = actual;
            break;

        case "D":
            model.ActualD = actual;
            break;

        case "E":
            model.ActualE = actual;
            break;

        case "F":
            model.ActualF = actual;
            break;
    }
}
