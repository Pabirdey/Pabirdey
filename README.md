public JsonResult Get_Bin_Position(string date, string shift)
{
    try
    {
        List<Furnace_High_line> list = new List<Furnace_High_line>();

        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string sql = @"SELECT TIMESTAMP, SHIFT, TAG_ID, TAG_VAL 
                           FROM DEMO.T_HIGHLINE_REPORT_DATA 
                           WHERE TIMESTAMP = TO_DATE(:dt,'DD/MM/YYYY') 
                           AND SHIFT = :shift";

            using (OracleCommand cmd = new OracleCommand(sql, con))
            {
                cmd.Parameters.Add(":dt", date);
                cmd.Parameters.Add(":shift", shift);

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        list.Add(new Furnace_High_line
                        {
                            CellId = dr["TAG_ID"].ToString(),
                            Value = dr["TAG_VAL"] == DBNull.Value ? "" : dr["TAG_VAL"].ToString()
                        });
                    }
                }
            }
        }

        return Json(new { success = true, data = list }, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}
