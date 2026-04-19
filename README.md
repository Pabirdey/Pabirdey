 string tdQuery = @"
                    SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON')
                    AND TIMESTAMP < TO_DATE(:FDate,'DD/MM/YYYY')
                    AND FURNACE = :furnace";

                        using (OracleCommand cmd = new OracleCommand(tdQuery, con))
                        {
                            cmd.Parameters.Add("fDate", fDate);
                            cmd.Parameters.Add("furnace", furnace);

                            using (OracleDataReader dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    prevActual = Convert.ToDecimal(dr[0]);
                                    prevReported = Convert.ToDecimal(dr[1]);
                                }
                            }
                        }
