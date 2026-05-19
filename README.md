 <script>         
        function Dis_CBF_TO_IBF_LDActualData(lsSelectedFDate) {
            debugger;
            $.ajax({
                url: '/HML/GetCbfToIbfActalTodate',
                type: 'GET',
                data: { prodDate: lsSelectedFDate },
                success: function (response) {
                    if (response.success) {                        
                        var data = response.data;
                        debugger;
                        $("#TXT_CTOG_LD1_TONS").val(Math.round(data.CTOG_LD1_TONS || 0));
                        $("#TXT_CTOG_LD2_TONS").val(Math.round(data.CTOG_LD2_TONS || 0));
                        $("#TXT_CTOG_LD3_TONS").val(Math.round(data.CTOG_LD3_TONS || 0));
                        $("#TXT_CTOG_MRDTP_TONS").val(Math.round(data.CTOG_MRDTP_TONS || 0));
                        $("#TXT_CTOH_LD1_TONS").val(Math.round(data.CTOH_LD1_TONS || 0));
                        $("#TXT_CTOH_LD2_TONS").val(Math.round(data.CTOH_LD2_TONS || 0));
                        $("#TXT_CTOH_LD3_TONS").val(Math.round(data.CTOH_LD3_TONS || 0));
                        $("#TXT_CTOH_MRDTP_TONS").val(Math.round(data.CTOH_MRDTP_TONS || 0));
                        $("#TXT_CTOI_LD1_TONS").val(Math.round(data.CTOI_LD1_TONS || 0));
                        $("#TXT_CTOI_LD2_TONS").val(Math.round(data.CTOI_LD2_TONS || 0));
                        $("#TXT_CTOI_LD3_TONS").val(Math.round(data.CTOI_LD3_TONS || 0));
                        $("#TXT_CTOI_MRDTP_TONS").val(Math.round(data.CTOI_MRDTP_TONS || 0));
                    }
                    else {

                        alert(response.message + "\n" + response.error);
                    }
                },
                error: function (xhr) {

                    alert("Error occurred while loading data.");
                }
            });
        }    
    </script>
       public JsonResult GetCbfToIbfActalTodate(string prodDate)
        {
            BFViewModel model = new BFViewModel();
            try
            {
                DateTime dt = DateTime.ParseExact(prodDate, "dd/MMM/yyyy", System.Globalization.CultureInfo.InvariantCulture);
                string formattedDate = dt.ToString("dd/MMM/yyyy").ToUpper();

                string query = @"SELECT SUM(CASE WHEN plant IN ('A-F','G') THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AG,
                                        SUM(CASE WHEN plant IN ('A-F','G') THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AG,
                                        SUM(CASE WHEN plant IN ('A-F','G') THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AG,
                                        SUM(CASE WHEN plant IN ('A-F','G') THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AG,
                                        SUM(CASE WHEN plant IN ('A-F','G','H') THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AH,
                                        SUM(CASE WHEN plant IN ('A-F','G','H') THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AH,
                                        SUM(CASE WHEN plant IN ('A-F','G','H') THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AH,
                                        SUM(CASE WHEN plant IN ('A-F','G','H') THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AH,
                                        SUM(CASE WHEN plant IN ('A-F','G','H','I') THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AI,
                                        SUM(CASE WHEN plant IN ('A-F','G','H','I') THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AI,
                                        SUM(CASE WHEN plant IN ('A-F','G','H','I') THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AI,
                                        SUM(CASE WHEN plant IN ('A-F','G','H','I') THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AI
                                        FROM DEMO.T_LADLE WHERE date_time >= TRUNC(:prodDate,'MON') AND date_time <= :prodDate";
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        cmd.BindByName = true;
                        cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = dt;
                        using (OracleDataReader dr = cmd.ExecuteReader())
                        {
                            if (dr.Read())
                            {
                                model.CTOG_LD1_TONS = dr["LD1_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AG"]);
                                model.CTOG_LD2_TONS = dr["LD2_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AG"]);
                                model.CTOG_LD3_TONS = dr["LD3_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AG"]);
                                model.CTOG_MRDTP_TONS = dr["MRD_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AG"]);
                                model.CTOH_LD1_TONS = dr["LD1_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AH"]);
                                model.CTOH_LD2_TONS = dr["LD2_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AH"]);
                                model.CTOH_LD3_TONS = dr["LD3_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AH"]);
                                model.CTOH_MRDTP_TONS = dr["MRD_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AH"]);
                                model.CTOI_LD1_TONS = dr["LD1_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AI"]);
                                model.CTOI_LD2_TONS = dr["LD2_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AI"]);
                                model.CTOI_LD3_TONS = dr["LD3_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AI"]);
                                model.CTOI_MRDTP_TONS = dr["MRD_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AI"]);
                            }
                        }
                    }
                }

                return Json(new
                {
                    status = true,
                    data = model
                }, JsonRequestBehavior.AllowGet);
            }
            catch (Exception ex)
            {
                return Json(new
                {
                    status = false,
                    message = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }
        }

