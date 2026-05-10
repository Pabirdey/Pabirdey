[HttpGet]
public JsonResult GetShiftData(string sDate, string sShift)
{
    object data = null;

    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        try
        {
            int vCount = 0;

            // =====================================
            // CHECK SIGNOFF
            // =====================================

            string countQuery = @"
                SELECT COUNT(*)
                FROM DEMO.T_BF_SIGNOFF
                WHERE SO_DATE  = TO_DATE(:SO_DATE,'YYYY-MM-DD')
                AND   SO_SHIFT = :SO_SHIFT
                AND   SO_PAGE  = 'COKE_UNLOADING'
                AND   SO_CHECK = 1";

            OracleCommand cmdCount =
                new OracleCommand(countQuery, con);

            cmdCount.Parameters.Add("SO_DATE",
                OracleDbType.Varchar2).Value = sDate;

            cmdCount.Parameters.Add("SO_SHIFT",
                OracleDbType.Varchar2).Value = sShift;

            vCount = Convert.ToInt32(
                cmdCount.ExecuteScalar());

            string userName = "";
            int soCheck = 0;

            // =====================================
            // IF SIGNOFF EXISTS
            // =====================================

            if (vCount > 0)
            {
                string query = @"
                    SELECT NAME, SO_CHECK
                    FROM DEMO.T_BF_SIGNOFF
                    WHERE SO_DATE  = TO_DATE(:SO_DATE,'YYYY-MM-DD')
                    AND   SO_SHIFT = :SO_SHIFT
                    AND   SO_PAGE  = 'COKE_UNLOADING'";

                OracleCommand cmd =
                    new OracleCommand(query, con);

                cmd.Parameters.Add("SO_DATE",
                    OracleDbType.Varchar2).Value = sDate;

                cmd.Parameters.Add("SO_SHIFT",
                    OracleDbType.Varchar2).Value = sShift;

                OracleDataReader dr = cmd.ExecuteReader();

                if (dr.Read())
                {
                    userName = dr["NAME"].ToString();

                    soCheck = Convert.ToInt32(
                        dr["SO_CHECK"]);
                }
            }

            // =====================================
            // CALL PROCEDURES
            // =====================================

            OracleCommand proc1 =
                new OracleCommand(
                    "PROC_POPULATE_COKEUNLOADING", con);

            proc1.CommandType =
                CommandType.StoredProcedure;

            proc1.Parameters.Add("P_DATE",
                OracleDbType.Date).Value =
                Convert.ToDateTime(sDate);

            proc1.Parameters.Add("P_SHIFT",
                OracleDbType.Varchar2).Value =
                sShift;

            proc1.ExecuteNonQuery();

            // =====================================

            OracleCommand proc2 =
                new OracleCommand(
                    "PROC_POPULATE_HIGHLINE_DATA", con);

            proc2.CommandType =
                CommandType.StoredProcedure;

            proc2.Parameters.Add("P_DATE",
                OracleDbType.Date).Value =
                Convert.ToDateTime(sDate);

            proc2.Parameters.Add("P_SHIFT",
                OracleDbType.Varchar2).Value =
                sShift;

            proc2.ExecuteNonQuery();

            // =====================================

            OracleCommand proc3 =
                new OracleCommand(
                    "PROC_POPULATE_RAWMATERIAL_POSI", con);

            proc3.CommandType =
                CommandType.StoredProcedure;

            proc3.Parameters.Add("P_DATE",
                OracleDbType.Date).Value =
                Convert.ToDateTime(sDate);

            proc3.Parameters.Add("P_SHIFT",
                OracleDbType.Varchar2).Value =
                sShift;

            proc3.ExecuteNonQuery();

            // =====================================

            OracleCommand proc4 =
                new OracleCommand(
                    "PROC_POPULATE_UNLOAD_REP", con);

            proc4.CommandType =
                CommandType.StoredProcedure;

            proc4.Parameters.Add("P_DATE",
                OracleDbType.Date).Value =
                Convert.ToDateTime(sDate);

            proc4.Parameters.Add("P_SHIFT",
                OracleDbType.Varchar2).Value =
                sShift;

            proc4.ExecuteNonQuery();

            // =====================================

            data = new
            {
                success = true,
                SIGNOFF_NAME = userName,
                SO_CHECK = soCheck,
                IS_SIGNOFF = vCount > 0
            };
        }

        catch (Exception ex)
        {
            data = new
            {
                success = false,
                message = ex.Message
            };
        }
    }

    return Json(data,
        JsonRequestBehavior.AllowGet);
}
