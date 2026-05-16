string tdQueryC = @"
                SELECT
                    DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL)),
                    DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED))
                FROM DEMO.T_BF_PRODUCTION_TRACKING
                WHERE TIMESTAMP >= TRUNC(:prodDate,'MON')
                AND TIMESTAMP <= :prodDate
                AND FURNACE='C'";

            using (OracleCommand cmd = new OracleCommand(tdQueryC, con))
            {
                cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = prodDate;

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    if (dr.Read())
                    {
                        model.ActualCTD = dr[0] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(dr[0]);
                        model.ReportedCTD = dr[1] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(dr[1]);
                    }
                }
            }
