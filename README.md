[HttpPost]
public JsonResult SaveData(List<GranshotModel> model)
{
    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        OracleTransaction trans = con.BeginTransaction();

        try
        {
            foreach (var item in model)
            {
                string chkSql = @"SELECT COUNT(*)
                                  FROM T_GRANSHOT
                                  WHERE SEQ_NO = :SEQ_NO";

                OracleCommand chkCmd = new OracleCommand(chkSql, con);
                chkCmd.Transaction = trans;
                chkCmd.Parameters.Add(":SEQ_NO", item.SEQ_NO);

                int count = Convert.ToInt32(chkCmd.ExecuteScalar());

                OracleCommand cmd = new OracleCommand();
                cmd.Connection = con;
                cmd.Transaction = trans;

                if (count > 0)
                {
                    // UPDATE
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
                        WHERE SEQ_NO = :SEQ_NO";
                }
                else
                {
                    // INSERT
                    cmd.CommandText = @"
                        INSERT INTO T_GRANSHOT
                        (
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

                cmd.Parameters.Add(":SEQ_NO", item.SEQ_NO);
                cmd.Parameters.Add(":CAST_NO", item.CAST_NO);
                cmd.Parameters.Add(":CAST_START_DT", item.CAST_START_DT);
                cmd.Parameters.Add(":CAST_END_DT", item.CAST_END_DT);
                cmd.Parameters.Add(":LADLE_NO", item.LADLE_NO);
                cmd.Parameters.Add(":LADLE_START_DT", item.LADLE_START_DT);
                cmd.Parameters.Add(":LADLE_END_DT", item.LADLE_END_DT);
                cmd.Parameters.Add(":ARRIVED_FROM", item.ARRIVED_FROM);
                cmd.Parameters.Add(":GROSS", item.GROSS);
                cmd.Parameters.Add(":TARE", item.TARE);
                cmd.Parameters.Add(":NET", item.NET);

                cmd.ExecuteNonQuery();
            }

            trans.Commit();

            return Json(new { success = true });
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