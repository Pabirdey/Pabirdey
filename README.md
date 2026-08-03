[HttpPost]
public JsonResult BFProdProcedure(DateTime p_date, string p_furnace)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // 1. DailyConsRates
            using (OracleCommand cmd = new OracleCommand("DEMO.PKG_BF_THEORETICAL_CALC.DailyConsRates", con))
            {
                cmd.CommandType = CommandType.StoredProcedure;
                cmd.Parameters.Add("vDte", OracleDbType.Date).Value = p_date;
                cmd.Parameters.Add("vFur", OracleDbType.Varchar2).Value = p_furnace;
                cmd.ExecuteNonQuery();
            }

            // 2. PROC_FURNACE_DERAILMENT
            try
            {
                using (OracleCommand cmd = new OracleCommand("DEMO.PROC_FURNACE_DERAILMENT", con))
                {
                    cmd.CommandType = CommandType.StoredProcedure;
                    cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = p_date;
                    cmd.ExecuteNonQuery();
                }
            }
            catch
            {
                // Equivalent to: WHEN OTHERS THEN NULL;
            }

            // 3. PROC_FURNACE_DELAY_ANALYSIS
            try
            {
                using (OracleCommand cmd = new OracleCommand("DEMO.PROC_FURNACE_DELAY_ANALYSIS", con))
                {
                    cmd.CommandType = CommandType.StoredProcedure;
                    cmd.Parameters.Add("P_DATE", OracleDbType.Date).Value = p_date;
                    cmd.ExecuteNonQuery();
                }
            }
            catch
            {
                // Equivalent to: WHEN OTHERS THEN NULL;
            }
        }

        return Json(new
        {
            status = true,
            message = "Calculated Over!"
        });
    }
    catch (Exception ex)
    {
        return Json(new
        {
            status = false,
            message = ex.Message
        });
    }
}
