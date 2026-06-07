public JsonResult GetProductionSummary(DateTime txtdt)
{
    ProductionSummaryModel model = new ProductionSummaryModel();

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        string sql = @"
            SELECT FUR_NAME,
                   DESTINATION,
                   ROUND(SUM(NET_WT),2) NETWT
            FROM DEMO.T_LADLE_DETAILS
            WHERE LADLE_FLEND_TIME >= TRUNC(:PDATE)+6/24
              AND LADLE_FLEND_TIME < TRUNC(:PDATE)+1+6/24
            GROUP BY FUR_NAME,DESTINATION";

        OracleCommand cmd = new OracleCommand(sql, con);
        cmd.Parameters.Add("PDATE", OracleDbType.Date).Value = txtdt;

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            string fur = dr["FUR_NAME"].ToString();
            string dest = dr["DESTINATION"].ToString();
            decimal wt = Convert.ToDecimal(dr["NETWT"]);

            if (fur == "C" && dest == "LD1") model.LD1C = wt;
            else if (fur == "C" && dest == "LD2") model.LD2C = wt;
            else if (fur == "C" && dest == "LD3") model.LD3C = wt;
            else if (fur == "C" && dest == "MRD") model.MRDC = wt;
            else if (fur == "C" && dest == "GRANSHOT") model.GRC = wt;

            else if (fur == "E" && dest == "LD1") model.LD1E = wt;
            else if (fur == "E" && dest == "LD2") model.LD2E = wt;
            else if (fur == "E" && dest == "LD3") model.LD3E = wt;
            else if (fur == "E" && dest == "MRD") model.MRDE = wt;
            else if (fur == "E" && dest == "GRANSHOT") model.GRE = wt;

            else if (fur == "F" && dest == "LD1") model.LD1F = wt;
            else if (fur == "F" && dest == "LD2") model.LD2F = wt;
            else if (fur == "F" && dest == "LD3") model.LD3F = wt;
            else if (fur == "F" && dest == "MRD") model.MRDF = wt;
            else if (fur == "F" && dest == "GRANSHOT") model.GRF = wt;

            else if (fur == "G" && dest == "LD1") model.LD1G = wt;
            else if (fur == "G" && dest == "LD2") model.LD2G = wt;
            else if (fur == "G" && dest == "LD3") model.LD3G = wt;
            else if (fur == "G" && dest == "MRD") model.MRDG = wt;
            else if (fur == "G" && dest == "GRANSHOT") model.GRG = wt;

            else if (fur == "H" && dest == "LD1") model.LD1H = wt;
            else if (fur == "H" && dest == "LD2") model.LD2H = wt;
            else if (fur == "H" && dest == "LD3") model.LD3H = wt;
            else if (fur == "H" && dest == "MRD") model.MRDH = wt;
            else if (fur == "H" && dest == "GRANSHOT") model.GRH = wt;

            else if (fur == "I" && dest == "LD1") model.LD1I = wt;
            else if (fur == "I" && dest == "LD2") model.LD2I = wt;
            else if (fur == "I" && dest == "LD3") model.LD3I = wt;
            else if (fur == "I" && dest == "MRD") model.MRDI = wt;
            else if (fur == "I" && dest == "GRANSHOT") model.GRI = wt;
        }
    }

    model.LD1TOT = model.LD1C + model.LD1E + model.LD1F;
    model.LD2TOT = model.LD2C + model.LD2E + model.LD2F;
    model.LD3TOT = model.LD3C + model.LD3E + model.LD3F;
    model.MRDTOT = model.MRDC + model.MRDE + model.MRDF;
    model.GRTOT  = model.GRC  + model.GRE  + model.GRF;

    return Json(model, JsonRequestBehavior.AllowGet);
}
