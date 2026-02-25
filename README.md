   public JsonResult GetTheoreticalProd(string FDate)
        {
            string value = "";                       
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string query = @"SELECT VALUE  FROM imtg.T_FURNACES_PROC_HM_PROD  WHERE TRUNC(TIMESTAMP) =:FDate AND TAG_ID =10426";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value= FDate;
                    OracleDataReader dr = cmd.ExecuteReader();
                    if (dr.Read())
                    {                      
                        value = dr["VALUE"].ToString();
                    }
                }
            }

            return Json(new {value = value }, JsonRequestBehavior.AllowGet);
        }
          function Display_Theoretical_Prod(fDate) {
            debugger;
            $.ajax({
                url: '/HML/GetTheoreticalProd',
                type: 'GET',
                data: {fdate: fDate },
                success: function (response) {
                    $("#txtTheoretical").val(response.value);
                },
                error: function (error) {
                    console.log(error);
                }                
            });
        }
