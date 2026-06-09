public JsonResult Save_Granshot_Details(GranshotViewModel model)
{
    try
    {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
            con.Open();

            foreach (var item in model.Details)
            {
                DateTime castStart =
                    GetActualDateTime(
                        model.ProductionDate,
                        model.Shift,
                        item.CAST_ST_TIME);

                DateTime castEnd =
                    GetActualDateTime(
                        model.ProductionDate,
                        model.Shift,
                        item.CAST_END_TIME);

                DateTime ladleStart =
                    GetActualDateTime(
                        model.ProductionDate,
                        model.Shift,
                        item.LADLE_FLST_TIME);

                DateTime ladleEnd =
                    GetActualDateTime(
                        model.ProductionDate,
                        model.Shift,
                        item.LADLE_FLEND_TIME);

                string sql = @"
                INSERT INTO T_GRANSHOT_DETAILS
                (
                    PROD_DATE,
                    SHIFT_CODE,
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
                    REASON_POURING
                )
                VALUES
                (
                    :PROD_DATE,
                    :SHIFT_CODE,
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
                    :REASON_POURING
                )";

                using (OracleCommand cmd = new OracleCommand(sql, con))
                {
                    cmd.Parameters.Add("PROD_DATE", OracleDbType.Date).Value = model.ProductionDate;
                    cmd.Parameters.Add("SHIFT_CODE", OracleDbType.Varchar2).Value = model.Shift;
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

                    cmd.ExecuteNonQuery();
                }
            }
        }

        return Json(new
        {
            success = true,
            message = "Data Saved Successfully"
        });
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        });
    }
}
