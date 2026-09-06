 string ThermalImage = null;
                        string ThermalImageQuery = @"select substr(THERMAL_IMAGING_CONDITION,1,4) image_condition from t_thermal_imaging where timestamp=:vDate  and TLC_NO_THERMAL_IMAGING=:vTrpNo";
                        using (OracleCommand ThermalImagecmd = new OracleCommand(ThermalImageQuery, con))
                        {
                            
                            ThermalImagecmd.Parameters.Add(":vdate", OracleDbType.Date).Value = MaxThermalTimestamp;
                            ThermalImagecmd.Parameters.Add(":vTrpNo", OracleDbType.Int32).Value = vTrp_No;
                            object value = ThermalImagecmd.ExecuteScalar();
                           
                        }
