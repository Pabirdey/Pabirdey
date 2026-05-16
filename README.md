}
                }
            }
        }

        // ==========================================
        // TD QUERY
        // ==========================================

        string tdQuery = @"
            SELECT
                DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL)) ACTUAL_TD,
                DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED)) REPORTED_TD
            FROM DEMO.T_BF_PRODUCTION_TRACKING
            WHERE TIMESTAMP >= TRUNC(:prodDate,'MON')
            AND TIMESTAMP <= :prodDate
            AND FURNACE = :furnace";

        using (OracleCommand cmd2 = new OracleCommand(tdQuery, con))
        {
            cmd2.Parameters.Add("prodDate", OracleDbType.Date).Value = dt;
            cmd2.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;

            using (OracleDataReader dr = cmd2.ExecuteReader())
            {
                if (dr.Read())
                {
                    decimal? actTD =
                        dr["ACTUAL_TD"] == DBNull.Value
                        ? (decimal?)null
                        : Convert.ToDecimal(dr["ACTUAL_TD"]);

                    decimal? repTD =
                        dr["REPORTED_TD"] == DBNull.Value
                        ? (decimal?)null
                        : Convert.ToDecimal(dr["REPORTED_TD"]);

                    switch (furnace)
                    {
                        case "C":
                            model.ACTUAL_C_TD = actTD;
                            model.REPORTED_C_TD = repTD;
                            break;

                        case "E":
                            model.ACTUAL_E_TD = actTD;
                            model.REPORTED_E_TD = repTD;
                            break;

                        case "F":
                            model.ACTUAL_F_TD = actTD;
                            model.REPORTED_F_TD = repTD;
                            break;
                    }
                }
            }
        }
    }
    catch (OracleException ex)
    {
        throw new Exception(
            $"Oracle DB Error while loading furnace {furnace}: {ex.Message}");
    }
    catch (Exception ex)
    {
        throw new Exception(
            $"Error while loading furnace {furnace}: {ex.Message}");
    }
}
