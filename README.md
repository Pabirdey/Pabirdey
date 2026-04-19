public JsonResult GetBFProductionData(string fDate)
{
    List<BFProductionRow> list = new List<BFProductionRow>();

    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // ===== TOTAL VARIABLES (Running Total) =====
            decimal totalActual = 0;
            decimal totalReported = 0;
            decimal totalBalance = 0;
            decimal totalActualTD = 0;
            decimal totalReportedTD = 0;

            // ===== COUNT CHECK =====
            int count = 0;

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

            string[] furnaces = { "C", "E", "F" };

            foreach (string furnace in furnaces)
            {
                BFProductionRow row = new BFProductionRow();
                row.Furnace = furnace;

                decimal actual = 0, reported = 0, balance = 0;
                decimal prevActual = 0, prevReported = 0;

                // ================= IF (DATA EXISTS) =================
                if (count > 0)
                {
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
                }
                // ================= ELSE (LADLE LOGIC) =================
                else
                {
                    string ladleQuery = @"
                        SELECT NVL(SUM(NET_WT),0)
                        FROM demo.t_ladle_details
                        WHERE LADLE_FLEND_TIME >= TO_DATE(:fDate,'DD-MM-YYYY') + 6/24
                        AND LADLE_FLEND_TIME < TO_DATE(:fDate,'DD-MM-YYYY') + 1 + 6/24
                        AND DESTINATION <> 'R'
                        AND fur_name = :furnace";

                    using (OracleCommand cmd = new OracleCommand(ladleQuery, con))
                    {
                        cmd.Parameters.Add("fDate", fDate);
                        cmd.Parameters.Add("furnace", furnace);

                        actual = Convert.ToDecimal(cmd.ExecuteScalar());
                    }
                }

                // ===== PREVIOUS TD =====
                string tdQuery = @"
                    SELECT NVL(SUM(ACTUAL),0), NVL(SUM(REPORTED),0)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP >= TRUNC(TO_DATE(:fDate,'DD-MM-YYYY'),'MON')
                    AND TIMESTAMP < TO_DATE(:fDate,'DD-MM-YYYY')
                    AND FURNACE = :furnace";

                using (OracleCommand cmd = new OracleCommand(tdQuery, con))
                {
                    cmd.Parameters.Add("fDate", fDate);
                    cmd.Parameters.Add("furnace", furnace);

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            prevActual = Convert.ToDecimal(dr[0]);
                            prevReported = Convert.ToDecimal(dr[1]);
                        }
                    }
                }

                // ===== FINAL TD =====
                decimal actualTD = prevActual + actual;
                decimal reportedTD = prevReported + reported;

                // ===== BALANCE =====
                string balQuery = @"
                    SELECT NVL(SUM(NVL(ACTUAL,0) - NVL(REPORTED,0)),0)
                    FROM DEMO.T_BF_PRODUCTION_TRACKING
                    WHERE TIMESTAMP >= TRUNC(TO_DATE(:fDate,'DD-MM-YYYY'),'MON')
                    AND TIMESTAMP < TO_DATE(:fDate,'DD-MM-YYYY')
                    AND FURNACE = :furnace";

                using (OracleCommand cmd = new OracleCommand(balQuery, con))
                {
                    cmd.Parameters.Add("fDate", fDate);
                    cmd.Parameters.Add("furnace", furnace);

                    balance = Convert.ToDecimal(cmd.ExecuteScalar());
                }

                // ===== ASSIGN =====
                row.Actual = actual;
                row.Reported = reported;
                row.Balance = balance;
                row.ActualTD = actualTD;
                row.ReportedTD = reportedTD;

                list.Add(row);

                // ===== RUNNING TOTAL =====
                totalActual += actual;
                totalReported += reported;
                totalBalance += balance;
                totalActualTD += actualTD;
                totalReportedTD += reportedTD;
            }

            // ===== TOTAL ROW =====
            BFProductionRow totalRow = new BFProductionRow();

            totalRow.Furnace = "TOTAL";
            totalRow.Actual = totalActual;
            totalRow.Reported = totalReported;
            totalRow.Balance = totalBalance;
            totalRow.ActualTD = totalActualTD;
            totalRow.ReportedTD = totalReportedTD;

            list.Add(totalRow);
        }
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        }, JsonRequestBehavior.AllowGet);
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
