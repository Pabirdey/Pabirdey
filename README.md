[HttpGet]
public JsonResult GetGranShotDetails(string txtdt, string txtshift, string txtfur)
{
    List<LadleDetailsModel> list = new List<LadleDetailsModel>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string sql = @"SELECT *
                       FROM IMTG.T_GRANSHOT_DETAILS
                       WHERE TIMESTAMP = TO_DATE(:txtdt,'DD-MM-YYYY')
                       AND SHIFT = :txtshift
                       AND AREA = :txtfur
                       ORDER BY CAST_NO";

        OracleCommand cmd = new OracleCommand(sql, con);
        cmd.Parameters.Add(":txtdt", txtdt);
        cmd.Parameters.Add(":txtshift", txtshift);
        cmd.Parameters.Add(":txtfur", txtfur);

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            list.Add(new LadleDetailsModel
            {
                CAST_NO = Convert.ToDecimal(dr["CAST_NO"]),
                CAST_ST_TIME = dr["CAST_ST_TIME"].ToString(),
                CAST_END_TIME = dr["CAST_END_TIME"].ToString(),
                TRP_NO = dr["TRP_NO"].ToString(),
                LADLE_FLST_TIME = dr["LADLE_FLST_TIME"].ToString(),
                LADLE_FLEND_TIME = dr["LADLE_FLEND_TIME"].ToString(),
                ARRIVED_FROM = dr["ARRIVED_FROM"].ToString(),
                GROSS_WT = dr["GROSS_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["GROSS_WT"]),
                TARE_WT = dr["TARE_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["TARE_WT"]),
                NET_WT = dr["NET_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["NET_WT"]),
                POURING_RATE = dr["POURING_RATE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["POURING_RATE"]),
                HMT = dr["HMT"].ToString(),
                REASON_POURING = dr["REASON_POURING"].ToString(),
                SEQ_NO = dr["SEQ_NO"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["SEQ_NO"])
            });
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
