public JsonResult GetLadleData(string prodDate)
{
    LadleModel model = new LadleModel();

    try
    {
        DateTime dt = Convert.ToDateTime(prodDate);

        string query = @"
            SELECT 
                SUM(CASE WHEN plant IN ('A-F','G') 
                         THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AG,

                SUM(CASE WHEN plant IN ('A-F','G') 
                         THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AG,

                SUM(CASE WHEN plant IN ('A-F','G') 
                         THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AG,

                SUM(CASE WHEN plant IN ('A-F','G') 
                         THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AG,

                SUM(CASE WHEN plant IN ('A-F','G','H') 
                         THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AH,

                SUM(CASE WHEN plant IN ('A-F','G','H') 
                         THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AH,

                SUM(CASE WHEN plant IN ('A-F','G','H') 
                         THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AH,

                SUM(CASE WHEN plant IN ('A-F','G','H') 
                         THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AH,

                SUM(CASE WHEN plant IN ('A-F','G','H','I') 
                         THEN LD1_TONS_ACTUAL ELSE 0 END) LD1_ACT_TD_AI,

                SUM(CASE WHEN plant IN ('A-F','G','H','I') 
                         THEN LD2_TONS_ACTUAL ELSE 0 END) LD2_ACT_TD_AI,

                SUM(CASE WHEN plant IN ('A-F','G','H','I') 
                         THEN LD3_TONS_ACTUAL ELSE 0 END) LD3_ACT_TD_AI,

                SUM(CASE WHEN plant IN ('A-F','G','H','I') 
                         THEN MRDTP_TONS_ACTUAL ELSE 0 END) MRD_ACT_TD_AI

            FROM demo.t_ladle
            WHERE date_time >= TRUNC(:prodDate,'MON')
            AND date_time <= :prodDate";

        using (OracleConnection con = new OracleConnection(connectionString))
        {
            con.Open();

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Parameters.Add("prodDate", OracleDbType.Date).Value = dt;

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    if (dr.Read())
                    {
                        model.LD1_ACT_TD_AG = dr["LD1_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AG"]);
                        model.LD2_ACT_TD_AG = dr["LD2_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AG"]);
                        model.LD3_ACT_TD_AG = dr["LD3_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AG"]);
                        model.MRD_ACT_TD_AG = dr["MRD_ACT_TD_AG"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AG"]);

                        model.LD1_ACT_TD_AH = dr["LD1_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AH"]);
                        model.LD2_ACT_TD_AH = dr["LD2_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AH"]);
                        model.LD3_ACT_TD_AH = dr["LD3_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AH"]);
                        model.MRD_ACT_TD_AH = dr["MRD_ACT_TD_AH"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AH"]);

                        model.LD1_ACT_TD_AI = dr["LD1_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD1_ACT_TD_AI"]);
                        model.LD2_ACT_TD_AI = dr["LD2_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD2_ACT_TD_AI"]);
                        model.LD3_ACT_TD_AI = dr["LD3_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["LD3_ACT_TD_AI"]);
                        model.MRD_ACT_TD_AI = dr["MRD_ACT_TD_AI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MRD_ACT_TD_AI"]);
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
