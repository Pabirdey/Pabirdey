[HttpPost]
        public JsonResult Save_Granshot_Details(string ProductionDate)
        {
            GranshotViewModel model = new GranshotViewModel();
            OracleConnection con = null;
            OracleTransaction trans = null;

            try
            {
                DateTime dt = DateTime.ParseExact(ProductionDate, "dd/MMM/yyyy", System.Globalization.CultureInfo.InvariantCulture);
                string formattedDate = dt.ToString("dd/MMM/yyyy").ToUpper();
                con = new OracleConnection(iMonitorWebUtils.msConRWString);
                con.Open();

                trans = con.BeginTransaction();

                foreach (var item in model.Details)
                {
                    DateTime castStart = GetActualDateTime(model.ProductionDate,model.Shift,item.CAST_ST_TIME);
                    DateTime castEnd = GetActualDateTime(model.ProductionDate,model.Shift,item.CAST_END_TIME);
                    DateTime ladleStart = GetActualDateTime(model.ProductionDate,model.Shift,item.LADLE_FLST_TIME);
                    DateTime ladleEnd = GetActualDateTime(model.ProductionDate,model.Shift,item.LADLE_FLEND_TIME);                    
                    string checkSql = @"SELECT COUNT(*) FROM T_GRANSHOT_DETAILS WHERE TIMESTAMP = :TIMESTAMP AND SHIFT = :SHIFT AND SEQ_NO = :SEQ_NO";
                    int count = 0;
                    using (OracleCommand cmdCheck = new OracleCommand(checkSql, con))
                    {
                        cmdCheck.BindByName = true;
                        cmdCheck.Transaction = trans;
                        cmdCheck.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = model.ProductionDate;
                        cmdCheck.Parameters.Add("SHIFT", OracleDbType.Varchar2).Value = model.Shift;
                        cmdCheck.Parameters.Add("SEQ_NO", OracleDbType.Varchar2).Value = item.SEQ_NO;
                        count = Convert.ToInt32(cmdCheck.ExecuteScalar());
                    }

                    if (count == 0)
                    {
                        // INSERT
                        string insertSql = @"
                INSERT INTO T_GRANSHOT_DETAILS
                (
                    TIMESTAMP,
                    SHIFT,
                    CAST_NO,
                    CAST_ST_TIME,
                    CAST_END_TIME,
                    TRP_NO,
                    LADLE_FLST_TIME,
                    LADLE_FLEND_TIME,
                    ARRIVED_FROM,
                    GROSS_WT,
                    TARE_WT,
                    NET_WT,
                    POURING_RATE,
                    HMT,
                    REASON_POURING,
                    SEQ_NO
                )
                VALUES
                (
                    :TIMESTAMP,
                    :SHIFT,
                    :CAST_NO,
                    :CAST_ST_TIME,
                    :CAST_END_TIME,
                    :TRP_NO,
                    :LADLE_FLST_TIME,
                    :LADLE_FLEND_TIME,
                    :ARRIVED_FROM,
                    :GROSS_WT,
                    :TARE_WT,
                    :NET_WT,
                    :POURING_RATE,
                    :HMT,
                    :REASON_POURING,
                    :SEQ_NO
                )";

                        using (OracleCommand cmd = new OracleCommand(insertSql, con))
                        {
                            cmd.BindByName = true;
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = model.ProductionDate;
                            cmd.Parameters.Add("SHIFT", OracleDbType.Varchar2).Value = model.Shift;
                            cmd.Parameters.Add("CAST_NO", OracleDbType.Varchar2).Value = item.CAST_NO;
                            cmd.Parameters.Add("CAST_ST_TIME", OracleDbType.TimeStamp).Value = castStart;
                            cmd.Parameters.Add("CAST_END_TIME", OracleDbType.TimeStamp).Value = castEnd;
                            cmd.Parameters.Add("TRP_NO", OracleDbType.Varchar2).Value = item.TRP_NO;
                            cmd.Parameters.Add("LADLE_FLST_TIME", OracleDbType.TimeStamp).Value = ladleStart;
                            cmd.Parameters.Add("LADLE_FLEND_TIME", OracleDbType.TimeStamp).Value = ladleEnd;
                            cmd.Parameters.Add("ARRIVED_FROM", OracleDbType.Varchar2).Value = item.ARRIVED_FROM;
                            cmd.Parameters.Add("GROSS_WT", OracleDbType.Decimal).Value = item.GROSS_WT;
                            cmd.Parameters.Add("TARE_WT", OracleDbType.Decimal).Value = item.TARE_WT;
                            cmd.Parameters.Add("NET_WT", OracleDbType.Decimal).Value = item.NET_WT;
                            cmd.Parameters.Add("POURING_RATE", OracleDbType.Decimal).Value = item.POURING_RATE;
                            cmd.Parameters.Add("HMT", OracleDbType.Int32).Value = item.HMT;
                            cmd.Parameters.Add("REASON_POURING", OracleDbType.Varchar2).Value = item.REASON_POURING;
                            cmd.Parameters.Add("SEQ_NO", OracleDbType.Varchar2).Value = item.SEQ_NO;
                            cmd.ExecuteNonQuery();
                        }
                    }
                    else
                    {
                        // UPDATE
                        string updateSql = @"
                UPDATE T_GRANSHOT_DETAILS
                SET
                    CAST_ST_TIME     = :CAST_ST_TIME,
                    CAST_END_TIME    = :CAST_END_TIME,
                    TRP_NO           = :TRP_NO,
                    LADLE_FLST_TIME  = :LADLE_FLST_TIME,
                    LADLE_FLEND_TIME = :LADLE_FLEND_TIME,
                    ARRIVED_FROM     = :ARRIVED_FROM,
                    GROSS_WT         = :GROSS_WT,
                    TARE_WT          = :TARE_WT,
                    NET_WT           = :NET_WT,
                    POURING_RATE     = :POURING_RATE,
                    HMT              = :HMT,
                    REASON_POURING   = :REASON_POURING
                WHERE TIMESTAMP = :TIMESTAMP
                AND SHIFT = :SHIFT
                AND SEQ_NO = :SEQ_NO";

                        using (OracleCommand cmd = new OracleCommand(updateSql, con))
                        {
                            cmd.BindByName = true;
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("CAST_ST_TIME", OracleDbType.TimeStamp).Value = castStart;
                            cmd.Parameters.Add("CAST_END_TIME", OracleDbType.TimeStamp).Value = castEnd;
                            cmd.Parameters.Add("TRP_NO", OracleDbType.Varchar2).Value = item.TRP_NO;
                            cmd.Parameters.Add("LADLE_FLST_TIME", OracleDbType.TimeStamp).Value = ladleStart;
                            cmd.Parameters.Add("LADLE_FLEND_TIME", OracleDbType.TimeStamp).Value = ladleEnd;
                            cmd.Parameters.Add("ARRIVED_FROM", OracleDbType.Varchar2).Value = item.ARRIVED_FROM;
                            cmd.Parameters.Add("GROSS_WT", OracleDbType.Decimal).Value = item.GROSS_WT;
                            cmd.Parameters.Add("TARE_WT", OracleDbType.Decimal).Value = item.TARE_WT;
                            cmd.Parameters.Add("NET_WT", OracleDbType.Decimal).Value = item.NET_WT;
                            cmd.Parameters.Add("POURING_RATE", OracleDbType.Decimal).Value = item.POURING_RATE;
                            cmd.Parameters.Add("HMT", OracleDbType.Int32).Value = item.HMT;
                            cmd.Parameters.Add("REASON_POURING", OracleDbType.Varchar2).Value = item.REASON_POURING;

                            cmd.Parameters.Add("TIMESTAMP", OracleDbType.Date).Value = model.ProductionDate;
                            cmd.Parameters.Add("SHIFT", OracleDbType.Varchar2).Value = model.Shift;
                            cmd.Parameters.Add("SEQ_NO", OracleDbType.Varchar2).Value = item.SEQ_NO;

                            cmd.ExecuteNonQuery();
                        }
                    }
                }

                trans.Commit();

                return Json(new
                {
                    success = true,
                    message = "Data Saved Successfully"
                });
            }
            catch (Exception ex)
            {
                if (trans != null)
                    trans.Rollback();

                return Json(new
                {
                    success = false,
                    message = ex.Message
                });
            }
            finally
            {
                if (con != null)
                {
                    con.Close();
                    con.Dispose();
                }
            }
        }
