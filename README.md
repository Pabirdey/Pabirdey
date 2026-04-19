string tdQuery = @"
    SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0)
    FROM DEMO.T_BF_PRODUCTION_TRACKING
    WHERE TIMESTAMP >= TRUNC(TO_DATE(:fDate,'DD/MM/YYYY'),'MON')
    AND TIMESTAMP < TO_DATE(:fDate,'DD/MM/YYYY')
    AND FURNACE = :furnace";

using (OracleCommand cmd = new OracleCommand(tdQuery, con))
{
    cmd.BindByName = true; // ✅ VERY IMPORTANT

    cmd.Parameters.Add("fDate", OracleDbType.Varchar2).Value = fDate;
    cmd.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;

    using (OracleDataReader dr = cmd.ExecuteReader())
    {
        if (dr.Read())
        {
            prevActual = dr.IsDBNull(0) ? 0 : Convert.ToDecimal(dr[0]);
            prevReported = dr.IsDBNull(1) ? 0 : Convert.ToDecimal(dr[1]);
        }
    }
}
