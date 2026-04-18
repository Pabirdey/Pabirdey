 string ladleCountQuery = @"SELECT COUNT(*)
                                               FROM DEMO.T_LADLE
                                               WHERE DATE_TIME = TO_DATE(:FDate,'DD/MM/YYYY')
                                               AND PLANT = :FURNACE";

                    int ladleCount = 0;

                    using (OracleCommand cmd = new OracleCommand(ladleCountQuery, con))
                    {
                        cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                        cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                        ladleCount = Convert.ToInt32(cmd.ExecuteScalar());
                    }

                    if (ladleCount > 0)
                    {
                        string ladleQuery = @"SELECT LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,
                                                     LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
                                              FROM DEMO.T_LADLE
                                              WHERE DATE_TIME = TO_DATE(:FDate,'DD/MM/YYYY')
                                              AND PLANT = :FURNACE";

                        using (OracleCommand cmd = new OracleCommand(ladleQuery, con))
                        {
                            cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                            using (var dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    LD1 = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                                    LD2 = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                                    LD3 = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                                    MRD = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);
                                    NOOFTP = dr["NOOFTP"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["NOOFTP"]);

                                    LD1_ACT = dr["LD1_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS_ACTUAL"]);
                                    LD2_ACT = dr["LD2_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS_ACTUAL"]);
                                    LD3_ACT = dr["LD3_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS_ACTUAL"]);
                                    MRD_ACT = dr["MRDTP_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS_ACTUAL"]);
                                }
                            }
                        }
                    }
