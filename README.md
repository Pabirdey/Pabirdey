 public JsonResult GetTonnageData(string date, string shift)
        {
            List<object> cokeList = new List<object>();
            List<object> nutList = new List<object>();
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string query = @"SELECT BUNKER,TON_C_SC,TON_E_SC,TON_F_SC,TON_C_NC,TON_E_NC,TON_F_NC
                         FROM imtg.T_BF_CK_CONTROL_UNLOADING WHERE TRUNC(TIMESTAMP)=TO_DATE(:date,'DD/MM/YYYY') AND SHIFT=:shift";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.BindByName = true;
                    cmd.Parameters.Add("date", date);
                    cmd.Parameters.Add("shift", shift);
                    OracleDataReader dr = cmd.ExecuteReader();

                    while (dr.Read())
                    {
                        var obj = new
                        {
                            BUNKER = dr["BUNKER"].ToString(),
                            TON_C_SC = dr["TON_C_SC"].ToString(),
                            TON_E_SC = dr["TON_E_SC"].ToString(),
                            TON_F_SC = dr["TON_F_SC"].ToString(),
                            TON_C_NC = dr["TON_C_NC"].ToString(),
                            TON_E_NC = dr["TON_E_NC"].ToString(),
                            TON_F_NC = dr["TON_F_NC"].ToString()
                        };

                        if (dr["TYPE"].ToString() == "COKE")
                            cokeList.Add(obj);
                        else
                            nutList.Add(obj);
                    }
                }
            }

            return Json(new { coke = cokeList, nut = nutList }, JsonRequestBehavior.AllowGet);
        }
