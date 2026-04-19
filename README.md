 public JsonResult GetATOIBFActualDataByFurnace(string fDate, decimal? repOnDt)
        {
            List<BF_Production> list = new List<BF_Production>();
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();                    
                    string query = @"
                SELECT 'A-F' AS PLANT, SUM(LD1_TONS_ACTUAL) LD1_TONS_ACT,SUM(LD2_TONS_ACTUAL) LD2_TONS_ACT, SUM(LD3_TONS_ACTUAL) LD3_TONS_ACT, SUM(MRDTP_TONS_ACTUAL) MRD_TP_TONS 
                FROM DEMO.T_LADLE WHERE PLANT = 'A-F' AND DATE_TIME >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND DATE_TIME <= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'))
                UNION ALL
                SELECT 'A-G' AS PLANT, SUM(LD1_TONS_ACTUAL) LD1_TONS_ACT,SUM(LD2_TONS_ACTUAL) LD2_TONS_ACT, SUM(LD3_TONS_ACTUAL) LD3_TONS_ACT, SUM(MRDTP_TONS_ACTUAL) MRD_TP_TONS 
                FROM DEMO.T_LADLE WHERE PLANT IN ('A-F','G') AND DATE_TIME >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND DATE_TIME <= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'))
                UNION ALL
                SELECT 'A-H' AS PLANT, SUM(LD1_TONS_ACTUAL) LD1_TONS_ACT, SUM(LD2_TONS_ACTUAL) LD2_TONS_ACT, SUM(LD3_TONS_ACTUAL) LD3_TONS_ACT, SUM(MRDTP_TONS_ACTUAL) MRD_TP_TONS 
                FROM DEMO.T_LADLE WHERE PLANT IN ('A-F','G','H') AND DATE_TIME >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND DATE_TIME <= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'))
                UNION ALL
                SELECT 'A-I' AS PLANT, SUM(LD1_TONS_ACTUAL) LD1_TONS_ACT, SUM(LD2_TONS_ACTUAL) LD2_TONS_ACT, SUM(LD3_TONS_ACTUAL) LD3_TONS_ACT, SUM(MRDTP_TONS_ACTUAL) MRD_TP_TONS 
                FROM DEMO.T_LADLE WHERE PLANT IN ('A-F','G','H','I') AND DATE_TIME >= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'),'MON') AND DATE_TIME <= TRUNC(TO_DATE(:FDate,'DD/MM/YYYY'))
                ORDER BY PLANT";
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {                        
                        cmd.Parameters.Add("FDate", fDate);
                        using (var dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                BF_Production row = new BF_Production();
                                row.ACT_PLANT = dr["PLANT"].ToString();
                                row.ACT_LD1_TONS = dr["LD1_TONS_ACT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_TONS_ACT"]);
                                row.ACT_LD2_TONS = dr["LD2_TONS_ACT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_TONS_ACT"]);
                                row.ACT_LD3_TONS = dr["LD3_TONS_ACT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_TONS_ACT"]);
                                row.ACT_MRD_TP_TONS = dr["MRD_TP_TONS"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_TP_TONS"]);
                                list.Add(row);
                            }
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                return Json(new { error = ex.Message }, JsonRequestBehavior.AllowGet);
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }
         function Dis_ATOIBFActualData(fDate) {
        $.ajax({
            url: '@Url.Action("GetATOIBFActualDataByFurnace", "HML")',
            type: 'GET',
            data: { fDate: fDate },
            success: function (data) {
                if (data.message) {
                    alert(data.message);
                    return;
                }
                data.forEach(function (item) {
                    if (item.ACT_PLANT === "A-F") {
                        debugger;
                        $("#ACT_PLANT").val(item.ACT_PLANT);
                        $("#ACT_LD1_TONS").val(item.ACT_LD1_TONS);
                        $("#ACT_LD2_TONS").val(item.ACT_LD2_TONS);
                        $("#ACT_LD3_TONS").val(item.ACT_LD3_TONS);
                        $("#ACT_MRD_TP_TONS").val(item.ACT_MRD_TP_TONS);
                    }
                    if (item.ACT_PLANT === "A-G") {
                        $("#ACT_PLANT").val(item.ACT_PLANT);
                        $("#ACT_LD1_TONS").val(item.ACT_LD1_TONS);
                        $("#ACT_LD2_TONS").val(item.ACT_LD2_TONS);
                        $("#ACT_LD3_TONS").val(item.ACT_LD3_TONS);
                        $("#ACT_MRD_TP_TONS").val(item.ACT_MRD_TP_TONS);
                    }
                    if (item.ACT_PLANT === "A-H") {
                        $("#ACT_PLANT").val(item.ACT_PLANT);
                        $("#ACT_LD1_TONS").val(item.ACT_LD1_TONS);
                        $("#ACT_LD2_TONS").val(item.ACT_LD2_TONS);
                        $("#ACT_LD3_TONS").val(item.ACT_LD3_TONS);
                        $("#ACT_MRD_TP_TONS").val(item.ACT_MRD_TP_TONS);
                    }
                    if (item.ACT_PLANT === "A-I") {
                        $("#ACT_LD1_TONS").val(item.ACT_PLANT);
                        $("#ACT_LD1_TONS").val(item.ACT_LD1_TONS);
                        $("#ACT_LD2_TONS").val(item.ACT_LD2_TONS);
                        $("#ACT_LD3_TONS").val(item.ACT_LD3_TONS);
                        $("#ACT_MRD_TP_TONS").val(item.ACT_MRD_TP_TONS);
                    }
                });

            }
        });

    }
