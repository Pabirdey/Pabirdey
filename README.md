        [HttpGet]
        public JsonResult CheckLotCount(string furName,string supplier)
        {
            int cnt = 0;
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();
                    if fur_name = 'C' && fur_name = 'B' && fur_name = 'C'
                    {
                        string sql = @"select count(lot_no) cnt from imtg.T_TAP_HOLE_CLAY where supplier ='+furName+' and fur_name='+furName+'  and bag_in_stock> 0";
                    }
                    else
                    {
                        string sql = @"select count(lot_no) cnt from imtg.T_TAP_HOLE_CLAY where supplier ='+furName+' and fur_name='+furName+'  and bag_in_stock> 0";
                    }
                    using (OracleCommand cmd = new OracleCommand(sql, con))
                    {
                        cmd.BindByName = true;
                        cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = furName;
                        cmd.Parameters.Add(":SUPPLIER", OracleDbType.Varchar2).Value = supplier;

                        cnt = Convert.ToInt32(cmd.ExecuteScalar());
                    }
                }
            }
            catch (Exception ex)
            {                
                return Json(-1, JsonRequestBehavior.AllowGet);
            }

            return Json(cnt, JsonRequestBehavior.AllowGet);
        }
