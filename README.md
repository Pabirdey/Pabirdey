 [HttpPost]
        public JsonResult DeleteCast(int seqNo)
        {           
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                string query = "DELETE FROM TEST.T_GRANSHOT_DETAILS WHERE SEQ_NO = :seqNo";
                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Parameters.Add(new OracleParameter("seqNo", seqNo));
                    int rows = cmd.ExecuteNonQuery();
                    if (rows > 0)
                        return Json(new { success = true });
                    else
                        return Json(new { success = false });
                }
            }
        }
