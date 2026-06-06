[HttpGet]
public JsonResult GetHotMetalAnalysis(string pdate, string pshift, string parea)
{
    List<HotMetalAnalysisModel> list = new List<HotMetalAnalysisModel>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string sql = @"
        SELECT
            H.CASTNO,
            H.TRP_NO TP,
            TO_CHAR(H.DATE_TIME,'DD-MON-YYYY HH24:MI') HOTMETAL_TIME,
            H.C,
            H.SI,
            H.S,
            H.MN,
            H.TI,
            H.P,
            H.CR,
            H.BORON
        FROM IMTG.T_GRANSHOT_DETAILS G
        CROSS APPLY
        (
            SELECT *
            FROM
            (
                SELECT *
                FROM IMTG.T_HOT_METAL_ANAL H
                WHERE H.FUR_NO =
                    DECODE(G.ARRIVED_FROM,
                           'C',3,'D',4,'E',5,
                           'F',6,'G',7,'H',8,'I',9)
                AND H.TRP_NO = G.TRP_NO
                AND H.DATE_TIME <= G.LADLE_FLEND_TIME
                ORDER BY H.DATE_TIME DESC
            )
            WHERE ROWNUM = 1
        ) H
        WHERE TRUNC(G.TIMESTAMP)=TO_DATE(:pdate,'DD/MM/YYYY')
        AND G.SHIFT=:pshift
        AND G.AREA=:parea
        ORDER BY G.LADLE_FLEND_TIME";

        OracleCommand cmd = new OracleCommand(sql, con);

        cmd.Parameters.Add(":pdate", pdate);
        cmd.Parameters.Add(":pshift", pshift);
        cmd.Parameters.Add(":parea", parea);

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            list.Add(new HotMetalAnalysisModel
            {
                CASTNO = dr["CASTNO"].ToString(),
                TP = dr["TP"].ToString(),
                HOTMETAL_TIME = dr["HOTMETAL_TIME"].ToString(),
                C = dr["C"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["C"]),
                SI = dr["SI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["SI"]),
                S = dr["S"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["S"]),
                MN = dr["MN"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["MN"]),
                TI = dr["TI"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["TI"]),
                P = dr["P"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["P"]),
                CR = dr["CR"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["CR"]),
                BORON = dr["BORON"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BORON"])
            });
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
