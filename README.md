int PlanScan = 0;

string PlanScan_query = @"
    SELECT COUNT(FILL_STATUS) AS TOTAL_RUNNING_HR
    FROM DEMO.T_LADLE_DETAILS
    WHERE LADLE_FLEND_TIME >= :vdate_Prev
      AND LADLE_FLEND_TIME <= :vdate
      AND TRP_NO = :vTrp_No
      AND RET_FLAG = 'N'";

using (OracleCommand PlanScanCmd =
       new OracleCommand(PlanScan_query, con))
{
    PlanScanCmd.BindByName = true;

    PlanScanCmd.Parameters.Add(":vdate_Prev", OracleDbType.Date)
        .Value = vdate_Prev;

    PlanScanCmd.Parameters.Add(":vdate", OracleDbType.Date)
        .Value = vdate;

    PlanScanCmd.Parameters.Add(":vTrp_No", OracleDbType.Int32)
        .Value = vTrp_No;

    object value = PlanScanCmd.ExecuteScalar();

    if (value != null && value != DBNull.Value)
    {
        PlanScan = Convert.ToInt32(value);
    }
    else
    {
        PlanScan = 0;
    }
}
