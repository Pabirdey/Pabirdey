public JsonResult GetATOFBFLDReportData(string fDate)
{
    List<BF_Production> list = new List<BF_Production>();

    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            bool recordExists = false;

            // ================= CHECK EXISTS =================
            string countQuery = @"SELECT 1 
                                  FROM demo.t_ladle 
                                  WHERE DATE_TIME = TO_DATE(:pDate,'DD/MM/YYYY') 
                                  AND PLANT = 'A-F'";

            using (OracleCommand cmd = new OracleCommand(countQuery, con))
            {
                cmd.BindByName = true;
                cmd.Parameters.Add("pDate", OracleDbType.Varchar2).Value = fDate;

                var result = cmd.ExecuteScalar();
                recordExists = (result != null);
            }

            string query = "";

            if (recordExists)
            {
                query = @"SELECT 
                            LD1_TONS,LD2_TONS,LD3_TONS,
                            MRDTP_TONS,NOOFTP
                          FROM demo.t_ladle 
                          WHERE DATE_TIME = TO_DATE(:pDate,'DD/MM/YYYY') 
                          AND PLANT = 'A-F'";
            }
            else
            {
                query = @"SELECT 
                        NVL(SUM(CASE WHEN DESTINATION = 'LD1' THEN NET_WT END), 0) AS LD1_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD2' THEN NET_WT END), 0) AS LD2_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD3' THEN NET_WT END), 0) AS LD3_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'MRD' AND TRP_NO <= 50 THEN NET_WT END), 0) AS MRDTP_TONS,
                        NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END), 0) AS NOOFTP
                    FROM demo.t_ladle_details
                    WHERE LADLE_FLEND_TIME >= TO_DATE(:pDate,'DD/MM/YYYY') + 6/24
                      AND LADLE_FLEND_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
                      AND FUR_NAME IN ('C','D','E','F')";
            }

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.BindByName = true;
                cmd.Parameters.Add("pDate", OracleDbType.Varchar2).Value = fDate;

                using (var dr = cmd.ExecuteReader())
                {
                    if (dr.Read()) // only 1 row expected
                    {
                        BF_Production row = new BF_Production();

                        row.LD1_TONS = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                        row.LD2_TONS = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                        row.LD3_TONS = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                        row.MRDTP_TONS = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);
                        row.NOOFTP = dr["NOOFTP"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["NOOFTP"]);

                        list.Add(row);
                    }
                }
            }
        }
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
