  public JsonResult GetFurnaceWiseTypeData(string furnace, string FDate)
        {           
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string query = @"SELECT COAL_TYPE,IO_TYPE,PYROXINITE_TYPE,LIMESTONE_TYPE FROM DEMO.T_BF_PRODUCTION_TEST WHERE TIMESTAMP =(SELECT MAX(TIMESTAMP) FROM DEMO.T_BF_PRODUCTION_TEST WHERE FUR_NO =:furnace AND TIMESTAMP<=to_date(:FDate,'DD/MM/YYYY') AND IO_TYPE IS NOT NULL) AND FUR_NO = :furnace";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add("furnace", furnace);
                    cmd.Parameters.Add("FDate", FDate);
                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            return Json(new
                            {
                                COAL_TYPE = dr["COAL_TYPE"].ToString(),
                                IO_TYPE = dr["IO_TYPE"].ToString(),
                                PYROXINITE_TYPE = dr["PYROXINITE_TYPE"].ToString(),
                                LIMESTONE_TYPE = dr["LIMESTONE_TYPE"].ToString()
                            }, JsonRequestBehavior.AllowGet);
                        }
                    }
                }
            }

            return Json(null, JsonRequestBehavior.AllowGet);
        }
