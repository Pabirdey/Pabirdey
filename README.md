string ThermalImage = null;

if (MaxThermalTimestamp.HasValue)
{
    string ThermalImageQuery = @"
        SELECT SUBSTR(THERMAL_IMAGING_CONDITION, 1, 4)
        FROM T_THERMAL_IMAGING
        WHERE TIMESTAMP = :vDate
          AND TLC_NO_THERMAL_IMAGING = :vTrpNo";

    using (OracleCommand cmd =
           new OracleCommand(ThermalImageQuery, con))
    {
        cmd.Parameters.Add(":vDate", OracleDbType.Date)
            .Value = MaxThermalTimestamp.Value;

        cmd.Parameters.Add(":vTrpNo", OracleDbType.Int32)
            .Value = vTrp_No;

        object value = cmd.ExecuteScalar();

        if (value != null && value != DBNull.Value)
        {
            ThermalImage = value.ToString();
        }
    }
}
