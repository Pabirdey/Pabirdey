public JsonResult GetBFProductionData(string fDate)
{
    BFProductionModel model = new BFProductionModel();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        model.DateTime = Convert.ToDateTime(fDate);

        int count = 0;

        // ===== COUNT CHECK =====
        string countQuery = @"
            SELECT COUNT(*)
            FROM DEMO.T_BF_PRODUCTION_TRACKING
            WHERE TIMESTAMP = TO_DATE(:fDate,'DD-MM-YYYY')
            AND FURNACE IN ('C','D','E','F')";

        using (OracleCommand cmd = new OracleCommand(countQuery, con))
        {
            cmd.Parameters.Add("fDate", fDate);
            count = Convert.ToInt32(cmd.ExecuteScalar());
        }

        // ===== IF EXISTS =====
        if (count > 0)
        {
            string[] furnaces = { "C", "E", "F" }; // add D if needed

            foreach (string furnace in furnaces)
            {
                decimal actual = 0, reported = 0, balance = 0;
                decimal actualTD = 0, reportedTD = 0;

                // ===== DAILY =====
                string dailyQuery = @"
                    SELECT NVL(ACTUAL,0), NVL(REPORTED,0), NVL(BALANCE,0)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP = TO_DATE(:fDate,'DD-MM-YYYY')
                    AND FURNACE = :furnace";

                using (OracleCommand cmd = new OracleCommand(dailyQuery, con))
                {
                    cmd.Parameters.Add("fDate", fDate);
                    cmd.Parameters.Add("furnace", furnace);

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            actual = Convert.ToDecimal(dr[0]);
                            reported = Convert.ToDecimal(dr[1]);
                            balance = Convert.ToDecimal(dr[2]);
                        }
                    }
                }

                // ===== TD =====
                string tdQuery = @"
                    SELECT 
                        DECODE(SUM(ACTUAL),0,NULL,SUM(ACTUAL)),
                        DECODE(SUM(REPORTED),0,NULL,SUM(REPORTED))
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP >= TRUNC(TO_DATE(:fDate,'DD-MM-YYYY'),'MON')
                    AND TIMESTAMP <= TO_DATE(:fDate,'DD-MM-YYYY')
                    AND FURNACE = :furnace";

                using (OracleCommand cmd = new OracleCommand(tdQuery, con))
                {
                    cmd.Parameters.Add("fDate", fDate);
                    cmd.Parameters.Add("furnace", furnace);

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            actualTD = dr.IsDBNull(0) ? 0 : Convert.ToDecimal(dr[0]);
                            reportedTD = dr.IsDBNull(1) ? 0 : Convert.ToDecimal(dr[1]);
                        }
                    }
                }

                // ===== MAP TO MODEL =====
                if (furnace == "C")
                {
                    model.ACTUAL_C = actual;
                    model.REPORTED_C = reported;
                    model.BALANCE_C = balance;
                    model.ACTUAL_C_TD = actualTD;
                    model.REPORTED_C_TD = reportedTD;
                }
                else if (furnace == "E")
                {
                    model.ACTUAL_E = actual;
                    model.REPORTED_E = reported;
                    model.BALANCE_E = balance;
                    model.ACTUAL_E_TD = actualTD;
                    model.REPORTED_E_TD = reportedTD;
                }
                else if (furnace == "F")
                {
                    model.ACTUAL_F = actual;
                    model.REPORTED_F = reported;
                    model.BALANCE_F = balance;
                    model.ACTUAL_F_TD = actualTD;
                    model.REPORTED_F_TD = reportedTD;
                }
            }

            // ===== TOTAL (A-F) =====
            model.DISPLAY_ACTUAL =
                model.ACTUAL_C + model.ACTUAL_D + model.ACTUAL_E + model.ACTUAL_F;

            model.DISPLAY_REPORTED =
                model.REPORTED_C + model.REPORTED_D + model.REPORTED_E + model.REPORTED_F;

            model.DISPLAY_BALANCE =
                model.BALANCE_C + model.BALANCE_D + model.BALANCE_E + model.BALANCE_F;

            // ===== BALANCE TD (C only as per your code) =====
            string balQuery = @"
                SELECT SUM(NVL(ACTUAL,0) - NVL(REPORTED,0))
                FROM DEMO.T_BF_PRODUCTION_TRACKING
                WHERE TIMESTAMP >= TRUNC(TO_DATE(:fDate,'DD-MM-YYYY'),'MON')
                AND TIMESTAMP < TO_DATE(:fDate,'DD-MM-YYYY')
                AND FURNACE = 'C'";

            using (OracleCommand cmd = new OracleCommand(balQuery, con))
            {
                cmd.Parameters.Add("fDate", fDate);
                model.BALANCE_C = Convert.ToDecimal(cmd.ExecuteScalar());
            }
        }
    }

    return Json(model, JsonRequestBehavior.AllowGet);
}
