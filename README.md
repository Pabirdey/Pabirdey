[HttpGet]
        public JsonResult GET_TLC_DAILY_REPORT()
        {
            List<TLCDailyReport> list = new List<TLCDailyReport>();
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    string query = @"SELECT TLC_NO, MATURITY_LIFE, TLC_SIZE FROM Demo.T_TLC_MASTER ORDER BY TLC_NO";

                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                        using (OracleDataReader dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                TLCDailyReport model = new TLCDailyReport();
                                if (dr["TLC_NO"] != DBNull.Value)
                                {
                                    model.TLC_NO = Convert.ToInt32(dr["TLC_NO"]);
                                }
                                if (dr["MATURITY_LIFE"] != DBNull.Value)
                                {
                                    model.MATURITY_LIFE = Convert.ToInt32(dr["MATURITY_LIFE"]);
                                }
                                if (dr["TLC_SIZE"] != DBNull.Value)
                                {
                                    model.TLC_SIZE = dr["TLC_SIZE"].ToString();
                                }

                                list.Add(model);
                            }
                        }
                    }
                }

                return Json(new
                {
                    success = true,
                    data = list
                }, JsonRequestBehavior.AllowGet);
            }
            catch (Exception ex)
            {
                return Json(new
                {
                    success = false,
                    message = ex.Message
                }, JsonRequestBehavior.AllowGet);
            }
        }
         sqlstr = "Select TLC_NO,TLC_ST_DATE,TLC_END_DATE,TLC_STATUS,TLC_CAMPAINE_NO,CUMM_RUNNING_HR,CUMM_RUNNING_WT,TOTAL_RUNNING_HR,TOTAL_RUNNING_WT,MATURITY,QTY_PER_TRIP"
   sqlstr = sqlstr + " from DEMO.T_TLC_DETAILS a, (select c.TLC_NO TLC_NO2,max(c.tlc_ST_DATE) tlc_St_date2,max(c.seqno)  seqno2 from DEMO.T_TLC_DETAILS c where  c.tlc_ST_DATE<'" & vdate & "' and TLC_STATUS<>'MID_TERM' group by C.TLC_NO ) b"
   sqlstr = sqlstr + " where a.tlc_no = " & vTrp_No & " And a.seqno = b.seqno2  order by TLC_END_DATE DESC both query merge
