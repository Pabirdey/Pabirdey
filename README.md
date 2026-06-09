[HttpPost]
public JsonResult Save_Granshot_Details(GranshotViewModel model)
{
    OracleConnection con = null;
    OracleTransaction trans = null;

    try
    {
        con = new OracleConnection(iMonitorWebUtils.msConRWString);
        con.Open();

        trans = con.BeginTransaction();

        foreach (var item in model.Details)
        {
            DateTime castStart = GetActualDateTime(
                model.ProductionDate,
                model.Shift,
                item.CAST_ST_TIME);

            DateTime castEnd = GetActualDateTime(
                model.ProductionDate,
                model.Shift,
                item.CAST_END_TIME);

            DateTime ladleStart = GetActualDateTime(
                model.ProductionDate,
                model.Shift,
                item.LADLE_FLST_TIME);

            DateTime ladleEnd = GetActualDateTime(
                model.ProductionDate,
                model.Shift,
                item.LADLE_FLEND_TIME);

            // CHECK RECORD EXISTS
            string checkSql = @"SELECT COUNT(*)
                                FROM T_GRANSHOT_DETAILS
                                WHERE PROD_DATE = :PROD_DATE
                                AND SHIFT_CODE = :SHIFT_CODE
                                AND CAST_NO = :CAST_NO";

            int count = 0;

            using (OracleCommand cmdCheck = new OracleCommand(checkSql, con))
            {
                cmdCheck.Transaction = trans;

                cmdCheck.Parameters.Add("PROD_DATE", OracleDbType.Date).Value = model.ProductionDate;
                cmdCheck.Parameters.Add("SHIFT_CODE", OracleDbType.Varchar2).Value = model.Shift;
                cmdCheck.Parameters.Add("CAST_NO", OracleDbType.Varchar2).Value = item.CAST_NO;

                count = Convert.ToInt32(cmdCheck.ExecuteScalar());
            }

            if (count == 0)
            {
                // INSERT
                string insertSql = @"
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

                using (OracleCommand cmd = new OracleCommand(insertSql, con))
                {
                    cmd.Transaction = trans;

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
                WHERE PROD_DATE = :PROD_DATE
                AND SHIFT_CODE = :SHIFT_CODE
                AND CAST_NO = :CAST_NO";

                using (OracleCommand cmd = new OracleCommand(updateSql, con))
                {
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

                    cmd.Parameters.Add("PROD_DATE", OracleDbType.Date).Value = model.ProductionDate;
                    cmd.Parameters.Add("SHIFT_CODE", OracleDbType.Varchar2).Value = model.Shift;
                    cmd.Parameters.Add("CAST_NO", OracleDbType.Varchar2).Value = item.CAST_NO;

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
