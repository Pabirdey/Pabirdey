   public JsonResult GetATOFBFLDReportData(string fDate)
        {
            List<BF_Production> list = new List<BF_Production>();

            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();                    
                    int v_temp = 0;
                    string countQuery = @"SELECT COUNT(*) 
                                  FROM demo.t_ladle 
                                  WHERE DATE_TIME = TO_DATE(:pDate,'DD/MM/YYYY') 
                                  AND PLANT = 'A-F'";

                    using (OracleCommand cmd = new OracleCommand(countQuery, con))
                    {
                        cmd.Parameters.Add("pDate", fDate);
                        v_temp = Convert.ToInt32(cmd.ExecuteScalar());
                    }                    
                    if (v_temp > 0)
                    {
                        string query = @"SELECT 
                                    DATE_TIME,PLANT,
                                    LD1_TONS,LD2_TONS,LD3_TONS,
                                    MRDTP_TONS,NOOFTP,
                                    LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,
                                    LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
                                 FROM demo.t_ladle 
                                 WHERE DATE_TIME = TO_DATE(:pDate,'DD/MM/YYYY') 
                                 AND PLANT = 'A-F'";

                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Parameters.Add("pDate", fDate);

                            using (var dr = cmd.ExecuteReader())
                            {
                                while (dr.Read())
                                {
                                    BF_Production row = new BF_Production();
                                    row.A_F_PLANT = dr["PLANT"].ToString();
                                    row.A_F_LD1_TONS = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                                    row.A_F_LD2_TONS = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                                    row.A_F_LD3_TONS = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                                    row.A_F_MRD_TP_TONS = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);
                                    row.ACT_A_F_TODT_LD1_TONS = dr["LD1_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS_ACTUAL"]);
                                    row.ACT_A_F_TODT_LD2_TONS = dr["LD2_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS_ACTUAL"]);
                                    row.ACT_A_F_TODT_LD3_TONS = dr["LD3_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS_ACTUAL"]);
                                    row.ACT_A_F_TODT_MRD_TP_TONS = dr["MRDTP_TONS_ACTUAL"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS_ACTUAL"]);
                                    list.Add(row);
                                }
                            }
                        }
                    }                    
                    else
                    {
                        string sqlquery = @"SELECT 
                        NVL(SUM(CASE WHEN DESTINATION = 'LD1' THEN NET_WT END), 0) AS LD1_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD2' THEN NET_WT END), 0) AS LD2_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD3' THEN NET_WT END), 0) AS LD3_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'MRD' AND TRP_NO <= 50 THEN NET_WT END), 0) AS MRDTP_TONS,
                        NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END), 0) AS NOOFTP
                    FROM demo.t_ladle_details
                    WHERE LADLE_FLEND_TIME >= TO_DATE(:pDate,'DD/MM/YYYY') + 6/24
                      AND LADLE_FLEND_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
                      AND FUR_NAME IN ('C','D','E','F')";

                        using (OracleCommand cmd = new OracleCommand(sqlquery, con))
                        {
                            cmd.Parameters.Add("pDate", fDate);

                            using (var dr = cmd.ExecuteReader())
                            {
                                while (dr.Read())
                                {
                                    BF_Production row = new BF_Production();

                                    row.A_F_PLANT = dr["PLANT"].ToString();
                                    row.A_F_LD1_TONS = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                                    row.A_F_LD2_TONS = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                                    row.A_F_LD3_TONS = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                                    row.A_F_MRD_TP_TONS = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);
                                    row.ACT_A_F_TODT_LD1_TONS = dr["LD1_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS"]);
                                    row.ACT_A_F_TODT_LD2_TONS = dr["LD2_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS"]);
                                    row.ACT_A_F_TODT_LD3_TONS = dr["LD3_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS"]);
                                    row.ACT_A_F_TODT_MRD_TP_TONS = dr["MRDTP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRDTP_TONS"]);
                                    list.Add(row);
                                }
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

         function Dis_ATOFBFLDReportData(fDate) {
        $.ajax({
            url: '@Url.Action("GetATOFBFLDReportData","HML")',
            type: 'GET',
            data: { fDate: fDate },
            success: function (data) {
                if (data.message) {
                    alert(data.message);
                    return;
                }
                data.forEach(function (item) {
                    if (item.FURNACE === "A-F") {
                        $("#A_F_PLANT").val(item.A_F_PLANT);
                        $("#A_F_LD1_TONS").val(item.A_F_LD1_TONS);
                        $("#A_F_LD2_TONS").val(item.A_F_LD2_TONS);
                        $("#A_F_LD3_TONS").val(item.A_F_LD3_TONS);
                        $("#A_F_MRD_TP_TONS").val(item.A_F_MRD_TP_TONS);
                        $("#ACT_A_F_TODT_LD1_TONS").val(item.ACT_A_F_TODT_LD1_TONS);
                        $("#ACT_A_F_TODT_LD2_TONS").val(item.ACT_A_F_TODT_LD2_TONS);
                        $("#ACT_A_F_TODT_LD3_TONS").val(item.ACT_A_F_TODT_LD3_TONS);
                        $("#ACT_A_F_TODT_MRD_TP_TONS").val(item.ACT_A_F_TODT_MRD_TP_TONS);
                    }
                    if (item.FURNACE === "G") {
                        $("#G_PLANT").val(item.G_PLANT);
                        $("#G_LD1_TONS").val(item.G_LD1_TONS);
                        $("#G_LD2_TONS").val(item.G_LD2_TONS);
                        $("#G_LD3_TONS").val(item.G_LD3_TONS);
                        $("#G_MRD_TP_TONS").val(item.G_MRD_TP_TONS);
                        $("#ACT_G_TODT_LD1_TONS").val(item.ACT_G_TODT_LD1_TONS);
                        $("#ACT_G_TODT_LD2_TONS").val(item.ACT_G_TODT_LD2_TONS);
                        $("#ACT_G_TODT_LD3_TONS").val(item.ACT_G_TODT_LD3_TONS);
                        $("#ACT_G_TODT_MRD_TP_TONS").val(item.ACT_G_TODT_MRD_TP_TONS);
                    }
                    if (item.FURNACE === "H") {
                        $("#H_PLANT").val(item.H_PLANT);
                        $("#H_LD1_TONS").val(item.H_LD1_TONS);
                        $("#H_LD2_TONS").val(item.H_LD2_TONS);
                        $("#H_LD3_TONS").val(item.H_LD3_TONS);
                        $("#H_MRD_TP_TONS").val(item.H_MRD_TP_TONS);
                        $("#ACT_H_TODT_LD1_TONS").val(item.ACT_H_TODT_LD1_TONS);
                        $("#ACT_H_TODT_LD2_TONS").val(item.ACT_H_TODT_LD2_TONS);
                        $("#ACT_H_TODT_LD3_TONS").val(item.ACT_H_TODT_LD3_TONS);
                        $("#ACT_H_TODT_MRD_TP_TONS").val(item.ACT_H_TODT_MRD_TP_TONS);
                    }
                    if (item.FURNACE === "I") {
                        $("#I_PLANT").val(item.I_PLANT);
                        $("#I_LD1_TONS").val(item.I_LD1_TONS);
                        $("#I_LD2_TONS").val(item.I_LD2_TONS);
                        $("#I_LD3_TONS").val(item.I_LD3_TONS);
                        $("#I_MRD_TP_TONS").val(item.I_MRD_TP_TONS);
                        $("#ACT_I_TODT_LD1_TONS").val(item.ACT_I_TODT_LD1_TONS);
                        $("#ACT_I_TODT_LD2_TONS").val(item.ACT_I_TODT_LD2_TONS);
                        $("#ACT_I_TODT_LD3_TONS").val(item.ACT_I_TODT_LD3_TONS);
                        $("#ACT_I_TODT_MRD_TP_TONS").val(item.ACT_I_TODT_MRD_TP_TONS);
                    }
                });               
            }
        });
    }
