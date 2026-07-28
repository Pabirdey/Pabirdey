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
                return Json(new { status = true, message = "Calculated Over!" });
            }
            catch (Exception ex)
            {
                return Json(new { status = false, message = ex.Message });
            }
        }
         function BFProdProcedure() {
        var furnaces = ["C","D", "E", "F"];        
        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/BF_Production/BFProdProcedure',
                type: 'POST',
                data: {
                    p_date: lsSelectedFDate,
                    p_furnace: furnace
                },
                success: function (res) {
                    alert("Calculated Over!");
                },
                error: function () {
                    alert(res.message);
                }
            });

        });
    }
