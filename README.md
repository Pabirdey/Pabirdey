public JsonResult GetFinesData()
{
    try
    {
        List<object> data = new List<object>();

        using (OracleConnection con = new OracleConnection("mycon"))
        {
            con.Open();

            string query = @"
            WITH latest AS (
                SELECT *
                FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
                WHERE SHIFT = (SELECT MAX(SHIFT) FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT)
                ORDER BY TIMESTAMP DESC
            )
            SELECT 'AL2O3' AS ELEMENT,
                   RETURN_FINES_AL2O3 AS RETURN_FINES,
                   WET_FINES_AL2O3 AS WET_FINES,
                   DRY_FINES_AL2O3 AS DRY_FINES,
                   DRY_FINES_500TPH_AL2O3 AS DRY_FINES_500TPH
            FROM latest WHERE ROWNUM = 1

            UNION ALL

            SELECT 'SIO2',
                   RETURN_FINES_SIO2,
                   WET_FINES_SIO2,
                   DRY_FINES_SIO2,
                   DRY_FINES_500TPH_SIO2
            FROM latest WHERE ROWNUM = 1

            UNION ALL

            SELECT 'P',
                   RETURN_FINES_P,
                   WET_FINES_P,
                   DRY_FINES_P,
                   DRY_FINES_500TPH_P
            FROM latest WHERE ROWNUM = 1

            UNION ALL

            SELECT 'K2O',
                   RETURN_FINES_K2O,
                   WET_FINES_K2O,
                   DRY_FINES_K2O,
                   DRY_FINES_500TPH_K2O
            FROM latest WHERE ROWNUM = 1
            ";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        data.Add(new
                        {
                            ELEMENT = dr["ELEMENT"] == DBNull.Value ? null : dr["ELEMENT"].ToString(),
                            RETURN_FINES = dr["RETURN_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["RETURN_FINES"]),
                            WET_FINES = dr["WET_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["WET_FINES"]),
                            DRY_FINES = dr["DRY_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES"]),
                            DRY_FINES_500TPH = dr["DRY_FINES_500TPH"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES_500TPH"])
                        });
                    }
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
