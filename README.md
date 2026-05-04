public JsonResult GetFinesData()
{
    try
    {
        List<object> data = new List<object>();

        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string query = @"
            SELECT 'AL2O3' ELEMENT, ROUND(RETURN_FINES_AL2O3,2) RETURN_FINES,
                   ROUND(WET_FINES_AL2O3,2) WET_FINES,
                   ROUND(DRY_FINES_AL2O3,2) DRY_FINES,
                   ROUND(DRY_FINES_500TPH_AL2O3,2) DRY_FINES_500TPH
            FROM (SELECT * FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT ORDER BY TIMESTAMP DESC) WHERE ROWNUM=1

            UNION ALL

            SELECT 'SIO2',
                   ROUND(RETURN_FINES_SIO2,2),
                   ROUND(WET_FINES_SIO2,2),
                   ROUND(DRY_FINES_SIO2,2),
                   ROUND(DRY_FINES_500TPH_SIO2,2)
            FROM (SELECT * FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT ORDER BY TIMESTAMP DESC) WHERE ROWNUM=1

            UNION ALL

            SELECT 'P',
                   ROUND(RETURN_FINES_P,3),
                   ROUND(WET_FINES_P,3),
                   ROUND(DRY_FINES_P,3),
                   ROUND(DRY_FINES_500TPH_P,3)
            FROM (SELECT * FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT ORDER BY TIMESTAMP DESC) WHERE ROWNUM=1

            UNION ALL

            SELECT 'K2O',
                   ROUND(RETURN_FINES_K2O,3),
                   ROUND(WET_FINES_K2O,3),
                   ROUND(DRY_FINES_K2O,3),
                   ROUND(DRY_FINES_500TPH_K2O,3)
            FROM (SELECT * FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT ORDER BY TIMESTAMP DESC) WHERE ROWNUM=1";

            using (OracleCommand cmd = new OracleCommand(query, con))
            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    data.Add(new
                    {
                        ELEMENT = dr["ELEMENT"].ToString(),
                        RETURN_FINES = dr["RETURN_FINES"],
                        WET_FINES = dr["WET_FINES"],
                        DRY_FINES = dr["DRY_FINES"],
                        DRY_FINES_500TPH = dr["DRY_FINES_500TPH"]
                    });
                }
            }
        }

        return Json(data, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new { error = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}
