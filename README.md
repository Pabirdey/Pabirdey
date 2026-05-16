private void LoadLadleSummary(
    OracleConnection con,
    DateTime prodDate,
    BlastFurnaceViewModel model)
{
    string query = @"
        SELECT
            NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT END),0) LD1,
            NVL(SUM(CASE WHEN DESTINATION='LD2' THEN NET_WT END),0) LD2,
            NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT END),0) LD3,
            NVL(SUM(CASE WHEN DESTINATION='MRD' THEN NET_WT END),0) MRD,
            NVL(SUM(FILL_STATUS),0) TP
        FROM DEMO.T_LADLE_DETAILS
        WHERE LADLE_FLEND_TIME >= :fromDate
        AND LADLE_FLEND_TIME < :toDate
        AND FUR_NAME IN ('C','D','E','F')";

    using (OracleCommand cmd = new OracleCommand(query, con))
    {
        cmd.Parameters.Add("fromDate", OracleDbType.Date)
            .Value = prodDate.AddHours(6);

        cmd.Parameters.Add("toDate", OracleDbType.Date)
            .Value = prodDate.AddDays(1).AddHours(6);

        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            if (dr.Read())
            {
                model.LD1Tons = Convert.ToDecimal(dr["LD1"]);
                model.LD2Tons = Convert.ToDecimal(dr["LD2"]);
                model.LD3Tons = Convert.ToDecimal(dr["LD3"]);
                model.MRDTPTons = Convert.ToDecimal(dr["MRD"]);
                model.NoOfTP = Convert.ToInt32(dr["TP"]);
            }
        }
    }
}
