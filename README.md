public JsonResult GetNextCastNo()
{
    int castNo = 0;
    int seqNo = 0;

    string sql = @"SELECT NVL(MAX(CAST_NO),0)+1 CAST_NO,
                          NVL(MAX(SEQ_NO),0)+1 SEQ_NO
                   FROM IMTG.T_GRANSHOT_DETAILS";

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        OracleCommand cmd = new OracleCommand(sql, con);
        OracleDataReader dr = cmd.ExecuteReader();

        if (dr.Read())
        {
            castNo = Convert.ToInt32(dr["CAST_NO"]);
            seqNo = Convert.ToInt32(dr["SEQ_NO"]);
        }
    }

    return Json(new
    {
        CAST_NO = castNo,
        SEQ_NO = seqNo
    }, JsonRequestBehavior.AllowGet);
}
