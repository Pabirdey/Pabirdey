public JsonResult GetTheoreticalProd(string FDate)
        {
            string value = "";                       
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string query = @"SELECT VALUE  FROM imtg.T_FURNACES_PROC_HM_PROD  WHERE TIMESTAMP = TO_DATE(':FDate','DD/MM/YYYY') AND TAG_ID =10426";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("FDate", FDate);
                    OracleDataReader dr = cmd.ExecuteReader();
                    if (dr.Read())
                    {                      
                        value = dr["VALUE"].ToString();
                    }
                }
            }

            return Json(new {value = value }, JsonRequestBehavior.AllowGet);
        }
