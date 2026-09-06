DateTime? maxTimestamp = null;

using (OracleCommand cmd = new OracleCommand(@"
    SELECT MAX(TIMESTAMP)
    FROM T_THERMAL_IMAGING
    WHERE TIMESTAMP >= :vStDate
      AND TIMESTAMP < :vTrvDate
      AND TLC_NO_THERMAL_IMAGING = :vTrpNo", con))
{
    cmd.Parameters.Add(":vStDate", OracleDbType.Date).Value = vStDate;
    cmd.Parameters.Add(":vTrvDate", OracleDbType.Date).Value = vtrvdate;
    cmd.Parameters.Add(":vTrpNo", OracleDbType.Int32).Value = vTrp_No;

    object value = cmd.ExecuteScalar();

    if (value != null && value != DBNull.Value)
        maxTimestamp = Convert.ToDateTime(value);
}
