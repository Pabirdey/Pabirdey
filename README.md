
                    string blendQuery = @"
                SELECT 
                    SUM(LD_Sludge), SUM(Mill_Scale), SUM(Flue_Dust), SUM(Esp_Dust),
                    SUM(Kiln_Dust), SUM(Gcp_Sludge), SUM(Lime_Fines), SUM(Wrp_MET),
                    SUM(LD_Slag_Fines), SUM(MILL_SLUDGE)
                FROM (
                    SELECT 
                        :vPSW1 * AVG(LD_Sludge) / 100 AS LD_Sludge,
                        :vPSW1 * AVG(Mill_Scale) / 100 AS Mill_Scale,
                        :vPSW1 * AVG(Flue_Dust) / 100 AS Flue_Dust,
                        :vPSW1 * AVG(Esp_Dust) / 100 AS Esp_Dust,
                        :vPSW1 * AVG(Kiln_Dust) / 100 AS Kiln_Dust,
                        :vPSW1 * AVG(Gcp_Sludge) / 100 AS Gcp_Sludge,
                        :vPSW1 * AVG(Lime_Fines) / 100 AS Lime_Fines,
                        :vPSW1 * AVG(WRP_MET) / 100 AS Wrp_MET,
                        :vPSW1 * AVG(LD_Slag_Fines) / 100 AS LD_Slag_Fines,
                        :vPSW1 * AVG(MILL_SLUDGE) / 100 AS MILL_SLUDGE
                    FROM T_PSW_DAILY
                    WHERE TRIM(SOURCE) = 'RMBB_KNR' AND TIMESTAMP >= TRUNC(:prepEndDate) - 200 AND BLEND_NO = :BL1                   
                )";

                    using (OracleCommand blendCmd = new OracleCommand(blendQuery, conn))
                    {
                        blendCmd.Parameters.Add(":vPSW1", OracleDbType.Decimal).Value = input.PSW1 ?? 0;
                        blendCmd.Parameters.Add(":prepEndDate", OracleDbType.Date).Value = input.EndDate;
                        blendCmd.Parameters.Add(":BL1", OracleDbType.Int32).Value = input.PSW_BL1 ?? 0;                        
                        using (OracleDataReader reader = blendCmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {

                                LD_Sludge_Cons = reader.IsDBNull(0) ?(decimal?) null : reader.GetDecimal(0);
                                Flue_Dust_Cons = reader.IsDBNull(1) ? (decimal?)null : reader.GetDecimal(1);
                                Esp_Dust_Cons = reader.IsDBNull(2) ? (decimal?)null : reader.GetDecimal(2);
                                Kiln_Dust_Cons = reader.IsDBNull(3) ? (decimal?)null : reader.GetDecimal(3);
                                Gcp_Sludge_Cons = reader.IsDBNull(4) ? (decimal?)null : reader.GetDecimal(4);
                                Lime_Fines_Cons = reader.IsDBNull(5) ? (decimal?)null : reader.GetDecimal(5);
                                Wrp_MET_Cons = reader.IsDBNull(6) ? (decimal?)null : reader.GetDecimal(6);
                                LD_Slag_Fines_Cons = reader.IsDBNull(7) ? (decimal?)null : reader.GetDecimal(7);
                                Mill_Sludge_Cons = reader.IsDBNull(8) ? (decimal?)null : reader.GetDecimal(8);
                            }
                        }
                    }
