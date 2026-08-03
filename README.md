[HttpPost]
        public JsonResult BFProdProcedure(DateTime p_date, string p_furnace)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    using (OracleCommand cmd = new OracleCommand("DEMO.PKG_BF_THEORETICAL_CALC.DailyConsRates", con))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;
                        cmd.Parameters.Add("vDte", OracleDbType.Date).Value = p_date;
                        cmd.Parameters.Add("vFur", OracleDbType.Varchar2).Value = p_furnace;
                        cmd.ExecuteNonQuery();
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
        Begin
				demo.proc_furnace_derailment(:ctl_blk.CTL_DATE_TIME_PROD);
			Exception
				when others then
				null;
			End;
		     Begin	
	DEMO.PROC_FURNACE_DELAY_ANALYSIS(:ctl_blk.CTL_DATE_TIME_PROD);  	
 	Exception
				when others then
				null;
			End;
