string balanceQuery = @"
            SELECT NVL(SUM(NVL(ACTUAL,0)
                   - NVL(REPORTED,0)),0) BALANCE
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
                    model.BALANCE_C = balance;
                    break;

                case "E":
                    model.BALANCE_E = balance;
                    break;

                case "F":
                    model.BALANCE_F = balance;
                    break;
            }
        }
    }
