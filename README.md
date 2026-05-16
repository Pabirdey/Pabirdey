private void LoadFurnaceData(
    OracleConnection con,
    DateTime prodDate,
    string furnace,
    BlastFurnaceViewModel model)
{
    try
    {
        string query = @"
            SELECT ACTUAL, REPORTED, BALANCE
            FROM DEMO.T_BF_PRODUCTION_TRACKING
            WHERE TIMESTAMP = :prodDate
            AND FURNACE = :furnace";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = prodDate;
            cmd.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                if (dr.Read())
                {
                    decimal actual = dr["ACTUAL"] == DBNull.Value
                        ? 0
                        : Convert.ToDecimal(dr["ACTUAL"]);

                    decimal reported = dr["REPORTED"] == DBNull.Value
                        ? 0
                        : Convert.ToDecimal(dr["REPORTED"]);

                    decimal balance = dr["BALANCE"] == DBNull.Value
                        ? 0
                        : Convert.ToDecimal(dr["BALANCE"]);

                    switch (furnace)
                    {
                        case "C":
                            model.ActualC = actual;
                            model.ReportedC = reported;
                            model.BalanceC = balance;
                            break;

                        case "D":
                            model.ActualD = actual;
                            model.ReportedD = reported;
                            model.BalanceD = balance;
                            break;

                        case "E":
                            model.ActualE = actual;
                            model.ReportedE = reported;
                            model.BalanceE = balance;
                            break;

                        case "F":
                            model.ActualF = actual;
                            model.ReportedF = reported;
                            model.BalanceF = balance;
                            break;
                    }
                }
            }
        }
    }
    catch (OracleException ex)
    {
        // Oracle specific exception
        throw new Exception(
            $"Oracle DB Error while loading furnace {furnace}: {ex.Message}");
    }
    catch (Exception ex)
    {
        // General exception
        throw new Exception(
            $"Error while loading furnace {furnace}: {ex.Message}");
    }
    finally
    {
        // Optional logging / cleanup
    }
}
