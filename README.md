public JsonResult GetATOIBFLDReportData(string fDate)
{
    List<BF_Production> list = new List<BF_Production>();
    string[] furnaces = { "A-F", "G", "H", "I" };

    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            foreach (var furnace in furnaces)
            {
                BF_Production row = new BF_Production();

                decimal LD1_TONS = 0, LD2_TONS = 0, LD3_TONS = 0;
                decimal MRDTP_TONS = 0, NOOFTP = 0;

                try
                {
                    // 🔹 Handle A-F group
                    string plantCondition = furnace == "A-F"
                        ? "IN ('C','D','E','F')"
                        : "= :FURNACE";

                    // =========================
                    // 🔴 CHECK DATA IN T_LADLE
                    // =========================
                    string countQuery = $@"
                        SELECT COUNT(*) 
                        FROM DEMO.T_LADLE 
                        WHERE DATE_TIME = TO_DATE(:FDate,'DD/MM/YYYY') 
                        AND PLANT {plantCondition}";

                    int count = 0;

                    using (OracleCommand cmd = new OracleCommand(countQuery, con))
                    {
                        cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;

                        if (furnace != "A-F")
                            cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                        count = Convert.ToInt32(cmd.ExecuteScalar());
                    }

                    // =========================
                    // 🔴 IF DATA EXISTS
                    // =========================
                    if (count > 0)
                    {
                        string sql = $@"
                            SELECT 
                                NVL(SUM(LD1_TONS),0),
                                NVL(SUM(LD2_TONS),0),
                                NVL(SUM(LD3_TONS),0),
                                NVL(SUM(MRDTP_TONS),0),
                                NVL(SUM(NOOFTP),0)
                            FROM DEMO.T_LADLE
                            WHERE DATE_TIME = TO_DATE(:FDate,'DD/MM/YYYY')
                            AND PLANT {plantCondition}";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;

                            if (furnace != "A-F")
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                            using (var dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    LD1_TONS = dr.IsDBNull(0) ? 0 : dr.GetDecimal(0);
                                    LD2_TONS = dr.IsDBNull(1) ? 0 : dr.GetDecimal(1);
                                    LD3_TONS = dr.IsDBNull(2) ? 0 : dr.GetDecimal(2);
                                    MRDTP_TONS = dr.IsDBNull(3) ? 0 : dr.GetDecimal(3);
                                    NOOFTP = dr.IsDBNull(4) ? 0 : dr.GetDecimal(4);
                                }
                            }
                        }
                    }
                    // =========================
                    // 🔴 ELSE (CALCULATE FROM DETAILS)
                    // =========================
                    else
                    {
                        string sql = $@"
                            SELECT 
                                NVL(SUM(CASE WHEN DESTINATION='LD1' THEN NET_WT END),0),
                                NVL(SUM(CASE WHEN DESTINATION='LD2' THEN NET_WT END),0),
                                NVL(SUM(CASE WHEN DESTINATION='LD3' THEN NET_WT END),0),
                                NVL(SUM(CASE WHEN DESTINATION='MRD' AND TRP_NO <= 50 THEN NET_WT END),0),
                                NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END),0)
                            FROM DEMO.T_LADLE_DETAILS
                            WHERE LADLE_FLEND_TIME >= TO_DATE(:FDate,'DD/MM/YYYY') + 6/24
                            AND LADLE_FLEND_TIME < TO_DATE(:FDate,'DD/MM/YYYY') + 1 + 6/24
                            AND FUR_NAME {plantCondition}";

                        using (OracleCommand cmd = new OracleCommand(sql, con))
                        {
                            cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;

                            if (furnace != "A-F")
                                cmd.Parameters.Add("FURNACE", OracleDbType.Varchar2).Value = furnace;

                            using (var dr = cmd.ExecuteReader())
                            {
                                if (dr.Read())
                                {
                                    LD1_TONS = dr.IsDBNull(0) ? 0 : dr.GetDecimal(0);
                                    LD2_TONS = dr.IsDBNull(1) ? 0 : dr.GetDecimal(1);
                                    LD3_TONS = dr.IsDBNull(2) ? 0 : dr.GetDecimal(2);
                                    MRDTP_TONS = dr.IsDBNull(3) ? 0 : dr.GetDecimal(3);
                                    NOOFTP = dr.IsDBNull(4) ? 0 : dr.GetDecimal(4);
                                }
                            }
                        }
                    }
                }
                catch (Exception ex)
                {
                    System.Diagnostics.Debug.WriteLine("Error: " + ex.Message);
                }

                // 🔹 ASSIGN TO OBJECT
                row.FURNACE = furnace;
                row.LD1_TONS = LD1_TONS;
                row.LD2_TONS = LD2_TONS;
                row.LD3_TONS = LD3_TONS;
                row.MRDTP_TONS = MRDTP_TONS;
                row.NOOFTP = NOOFTP;

                list.Add(row);
            }
        }
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
