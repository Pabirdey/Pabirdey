function Display_CTOFBFReportData(fDate) {
        $.ajax({
            url: '@Url.Action("GetCTOFBFReportDataByFurnace", "HML")',
            type: 'GET',
            data: { fDate: fDate },
            success: function (data) {            
                if (data.message) {
                    alert(data.message);
                    return;
                }

                data.forEach(function (item) {
                    if (item.FURNACE === "C") {
                        $("#CBF_ActOnDate").val(item.ACT_ONDT);
                        $("#CBF_ActToDate").val(item.ACT_TODT);
                        $("#CBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#CBF_ReportToDate").val(item.REPORT_TODT);
                        $("#CBF_Balance").val(item.BALANCE);
                    }

                    if (item.FURNACE === "E") {
                        $("#EBF_ActOnDate").val(item.ACT_ONDT);
                        $("#EBF_ActToDate").val(item.ACT_TODT);
                        $("#EBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#EBF_ReportToDate").val(item.REPORT_TODT);
                        $("#EBF_Balance").val(item.BALANCE);
                    }

                    if (item.FURNACE === "F") {
                        $("#FBF_ActOnDate").val(item.ACT_ONDT);
                        $("#FBF_ActToDate").val(item.ACT_TODT);
                        $("#FBF_ReportOnDate").val(item.REPORT_ONDT);
                        $("#FBF_ReportToDate").val(item.REPORT_TODT);
                        $("#FBF_Balance").val(item.BALANCE);
                    }

                });
            }
        });ublic JsonResult GetCTOFBFReportDataByFurnace(string fdate)
        {
            List<BF_Production> list = new List<BF_Production>();
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                // ================= COUNT =================
                int v_temp = 0;

                string countQuery = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS') AND FURNACE IN ('C','E','F')";
                using (OracleCommand cmd = new OracleCommand(countQuery, con))
                {
                    cmd.Parameters.Add("pDate", fdate);
                    v_temp = Convert.ToInt32(cmd.ExecuteScalar());
                }

                // ================= IF COUNT > 0 =================
                if (v_temp > 0)
                {
                    string query = @"SELECT a.FURNACE,a.ACTUAL AS ACT_ONDT,a.REPORTED AS REPORT_ONDT,a.BALANCE,(SELECT SUM(b.ACTUAL) FROM DEMO.T_BF_PRODUCTION_TRACKING b  WHERE b.FURNACE = a.FURNACE  AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')  AND b.TIMESTAMP <= a.TIMESTAMP) AS ACT_TODT,(SELECT SUM(b.REPORTED) FROM DEMO.T_BF_PRODUCTION_TRACKING b WHERE b.FURNACE = a.FURNACE AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON') AND b.TIMESTAMP <= a.TIMESTAMP) AS REPORT_TODT FROM DEMO.T_BF_PRODUCTION_TRACKING a WHERE a.TIMESTAMP = TO_DATE(:pDate,'YYYY-MM-DD HH24:MI:SS') AND a.FURNACE IN ('C','E','F') ORDER BY a.FURNACE";
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        cmd.Parameters.Add("pDate", fdate);

                        using (var dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                BF_Production row = new BF_Production();
                                row.FURNACE = dr["FURNACE"].ToString();
                                row.ACT_ONDT = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);
                                row.ACT_TODT = dr["ACT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT"]);
                                row.REPORT_ONDT = dr["REPORT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_ONDT"]);
                                row.REPORT_TODT = dr["REPORT_TODT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT"]);
                                row.BALANCE = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);                                                             
                                list.Add(row);
                            }
                        }
                    }
                }
                else
                {                    
                    return Json(new { message = "No Data Found" }, JsonRequestBehavior.AllowGet);
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }

    }
