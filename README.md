[HttpPost]
public JsonResult Save_Exception_Cast(List<dynamic> data)
{
    string connectionString =
        ConfigurationManager.ConnectionStrings["OracleConn"].ConnectionString;

    using (OracleConnection con = new OracleConnection(connectionString))
    {
        con.Open();

        for (int i = 0; i < data.Count; i++)
        {
            string idNo = Convert.ToString(data[i].ID_NO);
            string castDate = Convert.ToString(data[i].CAST_DATE);
            string hh24 = Convert.ToString(data[i].HH24);
            string mm = Convert.ToString(data[i].MM);

            // Skip empty rows
            if (string.IsNullOrEmpty(idNo) || string.IsNullOrEmpty(castDate))
                continue;

            // 1️⃣ CHECK RECORD EXISTS
            string chkSql =
                "SELECT COUNT(1) FROM T_EXCEPTION_CAST WHERE ID_NO = :ID_NO";

            OracleCommand chkCmd = new OracleCommand(chkSql, con);
            chkCmd.Parameters.Add(":ID_NO", idNo);

            int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());

            if (cnt > 0)
            {
                // 2️⃣ UPDATE
                string updSql = @"
                    UPDATE T_EXCEPTION_CAST
                    SET CAST_DATE =
                        TO_DATE(:CAST_DATE || ' ' || :HH24 || ':' || :MM,
                                'DD/MM/YYYY HH24:MI'),
                        HH24 = :HH24,
                        MM   = :MM
                    WHERE ID_NO = :ID_NO";

                OracleCommand updCmd = new OracleCommand(updSql, con);
                updCmd.Parameters.Add(":CAST_DATE", castDate);
                updCmd.Parameters.Add(":HH24", hh24);
                updCmd.Parameters.Add(":MM", mm);
                updCmd.Parameters.Add(":ID_NO", idNo);

                updCmd.ExecuteNonQuery();
            }
            else
            {
                // 3️⃣ INSERT
                string insSql = @"
                    INSERT INTO T_EXCEPTION_CAST
                    (ID_NO, CAST_DATE, HH24, MM)
                    VALUES
                    (:ID_NO,
                     TO_DATE(:CAST_DATE || ' ' || :HH24 || ':' || :MM,
                             'DD/MM/YYYY HH24:MI'),
                     :HH24,
                     :MM)";

                OracleCommand insCmd = new OracleCommand(insSql, con);
                insCmd.Parameters.Add(":ID_NO", idNo);
                insCmd.Parameters.Add(":CAST_DATE", castDate);
                insCmd.Parameters.Add(":HH24", hh24);
                insCmd.Parameters.Add(":MM", mm);

                insCmd.ExecuteNonQuery();
            }
        }
    }

    return Json("Insert / Update completed successfully");
}