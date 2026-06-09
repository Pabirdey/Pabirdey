[HttpPost]
public JsonResult SaveData(List<GranshotModel> model)
{
    string conStr = ConfigurationManager
                    .ConnectionStrings["OracleConn"]
                    .ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        OracleTransaction trans = con.BeginTransaction();

        try
        {
            foreach (var item in model)
            {
                string checkSql = @"
                    SELECT COUNT(*)
                    FROM T_GRANSHOT
                    WHERE PROD_DATE = :PROD_DATE
                    AND SHIFT = :SHIFT
                    AND AREA = :AREA
                    AND SEQ_NO = :SEQ_NO";

                OracleCommand checkCmd = new OracleCommand(checkSql, con);
                checkCmd.Transaction = trans;

                checkCmd.Parameters.Add(":PROD_DATE", OracleDbType.Date).Value = item.PROD_DATE;
                checkCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = item.SHIFT;
                checkCmd.Parameters.Add(":AREA", OracleDbType.Varchar2).Value = item.AREA;
                checkCmd.Parameters.Add(":SEQ_NO", OracleDbType.Int32).Value = item.SEQ_NO;

                int count = Convert.ToInt32(checkCmd.ExecuteScalar());

                OracleCommand cmd = new OracleCommand();
                cmd.Connection = con;
                cmd.Transaction = trans;

                if (count > 0)
                {
                    cmd.CommandText = @"
                        UPDATE T_GRANSHOT
                        SET CAST_NO = :CAST_NO,
                            CAST_START_DT = :CAST_START_DT,
                            CAST_END_DT = :CAST_END_DT,
                            LADLE_NO = :LADLE_NO,
                            LADLE_START_DT = :LADLE_START_DT,
                            LADLE_END_DT = :LADLE_END_DT,
                            ARRIVED_FROM = :ARRIVED_FROM,
                            GROSS = :GROSS,
                            TARE = :TARE,
                            NET = :NET
                        WHERE PROD_DATE = :PROD_DATE
                        AND SHIFT = :SHIFT
                        AND AREA = :AREA
                        AND SEQ_NO = :SEQ_NO";
                }
                else
                {
                    cmd.CommandText = @"
                        INSERT INTO T_GRANSHOT
                        (
                            PROD_DATE,
                            SHIFT,
                            AREA,
                            SEQ_NO,
                            CAST_NO,
                            CAST_START_DT,
                            CAST_END_DT,
                            LADLE_NO,
                            LADLE_START_DT,
                            LADLE_END_DT,
                            ARRIVED_FROM,
                            GROSS,
                            TARE,
                            NET
                        )
                        VALUES
                        (
                            :PROD_DATE,
                            :SHIFT,
                            :AREA,
                            :SEQ_NO,
                            :CAST_NO,
                            :CAST_START_DT,
                            :CAST_END_DT,
                            :LADLE_NO,
                            :LADLE_START_DT,
                            :LADLE_END_DT,
                            :ARRIVED_FROM,
                            :GROSS,
                            :TARE,
                            :NET
                        )";
                }

                cmd.Parameters.Add(":PROD_DATE", OracleDbType.Date).Value = item.PROD_DATE;
                cmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = item.SHIFT;
                cmd.Parameters.Add(":AREA", OracleDbType.Varchar2).Value = item.AREA;
                cmd.Parameters.Add(":SEQ_NO", OracleDbType.Int32).Value = item.SEQ_NO;

                cmd.Parameters.Add(":CAST_NO", OracleDbType.Varchar2).Value =
                    item.CAST_NO ?? "";

                cmd.Parameters.Add(":CAST_START_DT", OracleDbType.Date).Value =
                    item.CAST_START_DT;

                cmd.Parameters.Add(":CAST_END_DT", OracleDbType.Date).Value =
                    item.CAST_END_DT;

                cmd.Parameters.Add(":LADLE_NO", OracleDbType.Varchar2).Value =
                    item.LADLE_NO ?? "";

                cmd.Parameters.Add(":LADLE_START_DT", OracleDbType.Date).Value =
                    item.LADLE_START_DT;

                cmd.Parameters.Add(":LADLE_END_DT", OracleDbType.Date).Value =
                    item.LADLE_END_DT;

                cmd.Parameters.Add(":ARRIVED_FROM", OracleDbType.Varchar2).Value =
                    item.ARRIVED_FROM ?? "";

                cmd.Parameters.Add(":GROSS", OracleDbType.Decimal).Value =
                    item.GROSS;

                cmd.Parameters.Add(":TARE", OracleDbType.Decimal).Value =
                    item.TARE;

                cmd.Parameters.Add(":NET", OracleDbType.Decimal).Value =
                    item.NET;

                cmd.ExecuteNonQuery();
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
            trans.Rollback();

            return Json(new
            {
                success = false,
                message = ex.Message
            });
        }
    }
}