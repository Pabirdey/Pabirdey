DateTime? MaxThermalTimestamp = null;
                        string ThermalQuery = @" SELECT MAX(TIMESTAMP)FROM T_THERMAL_IMAGING WHERE TIMESTAMP >=trunc(:vStDate) AND TIMESTAMP <trunc(:vdate) AND TLC_NO_THERMAL_IMAGING = :vTrpNo";
                        using (OracleCommand Thermalcmd = new OracleCommand(ThermalQuery, con))
                        {
                            Thermalcmd.Parameters.Add(":vStDate", OracleDbType.Date).Value = finalDate;
                            Thermalcmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate;
                            Thermalcmd.Parameters.Add(":vTrpNo", OracleDbType.Int32).Value = vTrp_No;
                            object value = cmd.ExecuteScalar();
                            if (value != null && value != DBNull.Value)
                                MaxThermalTimestamp = Convert.ToDateTime(value);
                        }
