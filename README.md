[HttpPost]
public JsonResult DeleteCast(int seqNo)
{
    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        OracleTransaction txn = con.BeginTransaction();  // ✅ START TRANSACTION

        try
        {
            string query = "DELETE FROM TEST.T_GRANSHOT_DETAILS WHERE SEQ_NO = :seqNo";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Transaction = txn; // ✅ attach transaction

                cmd.Parameters.Add(new OracleParameter("seqNo", seqNo));

                int rows = cmd.ExecuteNonQuery();

                if (rows > 0)
                {
                    txn.Commit(); // ✅ SUCCESS COMMIT
                    return Json(new { success = true });
                }
                else
                {
                    txn.Rollback(); // ❌ NOTHING DELETED
                    return Json(new { success = false });
                }
            }
        }
        catch (Exception ex)
        {
            txn.Rollback(); // ❌ ERROR → ROLLBACK

            return Json(new
            {
                success = false,
                message = ex.Message
            });
        }
    }
}
