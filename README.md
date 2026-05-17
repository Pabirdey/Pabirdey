 string balanceQuery = @"
            SELECT NVL(
                    SUM(NVL(ACTUAL,0) - NVL(REPORTED,0)),
                    0
                   ) BALANCE
            FROM DEMO.T_BF_PRODUCTION_TRACKING
            WHERE TIMESTAMP >= TRUNC(:prodDate,'MON')
            AND TIMESTAMP < :prodDate
            AND FURNACE = :furnace";

        using (OracleCommand cmd3 =
            new OracleCommand(balanceQuery, con))
        {
            cmd3.BindByName = true;

            cmd3.Parameters.Add("prodDate",
                OracleDbType.Date).Value = dt;

            cmd3.Parameters.Add("furnace",
                OracleDbType.Varchar2).Value = furnace;

            decimal balance =
                Convert.ToDecimal(cmd3.ExecuteScalar());

            switch (furnace)
            {
                case "C":
                    model.BalanceC = balance;
                    break;

                case "E":
                    model.BalanceE = balance;
                    break;

                case "F":
                    model.BalanceF = balance;
                    break;
            }
        }
    }
    catch (OracleException ex)
    {
        throw new Exception(
            $"Oracle DB Error while loading ladle data for furnace {furnace}: {ex.Message}");
    }
    catch (Exception ex)
    {
        throw new Exception(
            $"Error while loading ladle data for furnace {furnace}: {ex.Message}");
    }
    finally
    {
        // Optional cleanup/logging
    }
}
