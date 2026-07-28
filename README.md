if (!recordFound)
{
    string detailQuery = "";

    if (furnace == "A-F")
    {
        detailQuery = @"
            SELECT
                NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT ELSE 0 END),0) LD1,
                NVL(SUM(CASE WHEN DESTINATION='LD2' THEN NET_WT ELSE 0 END),0) LD2,
                NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT ELSE 0 END),0) LD3,
                NVL(SUM(CASE WHEN DESTINATION='MRD' THEN NET_WT ELSE 0 END),0) MRD,
                NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG='N' THEN FILL_STATUS ELSE 0 END),0) NOOFTP
            FROM DEMO.T_LADLE_DETAILS
            WHERE LADLE_FLEND_TIME >= :fromDate
              AND LADLE_FLEND_TIME < :toDate
              AND FUR_NAME IN ('C','D','E','F')";
    }
    else
    {
        detailQuery = @"
            SELECT
                NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT ELSE 0 END),0) LD1,
                NVL(SUM(CASE WHEN DESTINATION='LD2' THEN NET_WT ELSE 0 END),0) LD2,
                NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT ELSE 0 END),0) LD3,
                NVL(SUM(CASE WHEN DESTINATION='MRD' THEN NET_WT ELSE 0 END),0) MRD,
                NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG='N' THEN FILL_STATUS ELSE 0 END),0) NOOFTP
            FROM DEMO.T_LADLE_DETAILS
            WHERE LADLE_FLEND_TIME >= :fromDate
              AND LADLE_FLEND_TIME < :toDate
              AND FUR_NAME = :furnace";
    }

    using (OracleCommand cmd = new OracleCommand(detailQuery, con))
    {
        cmd.BindByName = true;

        cmd.Parameters.Add("fromDate", OracleDbType.Date).Value = dt.AddHours(6);
        cmd.Parameters.Add("toDate", OracleDbType.Date).Value = dt.AddDays(1).AddHours(6);

        if (furnace != "A-F")
        {
            cmd.Parameters.Add("furnace", OracleDbType.Varchar2).Value = furnace;
        }

        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            if (dr.Read())
            {
                ld1 = dr["LD1"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1"]);
                ld2 = dr["LD2"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2"]);
                ld3 = dr["LD3"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3"]);
                mrd = dr["MRD"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD"]);
                nooftp = dr["NOOFTP"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["NOOFTP"]);

                ld1Act = ld1;
                ld2Act = ld2;
                ld3Act = ld3;
                mrdAct = mrd;
            }
        }
    }
}
