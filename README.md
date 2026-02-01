[HttpPost]
public JsonResult Save_Exception_Cast(List<dynamic> data)
{
    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        for (int i = 0; i < data.Count; i++)
        {
            string idNo     = Convert.ToString(data[i].ID_NO);
            string furnace  = Convert.ToString(data[i].FURNACE);
            string castDate = Convert.ToString(data[i].CAST_DATE);
            string hh24     = Convert.ToString(data[i].HH24);
            string mm       = Convert.ToString(data[i].MM);

            // 1️⃣ Skip invalid rows
            if (string.IsNullOrEmpty(idNo) ||
                string.IsNullOrEmpty(furnace) ||
                string.IsNullOrEmpty(castDate))
            {
                continue;
            }

            // 2️⃣ CHECK (ID_NO + FURNACE)
            string chkSql = @"
                SELECT COUNT(1)
                FROM Test.T_CAST_EXCEPTION
                WHERE ID_NO = :P_ID
                  AND FURNACE = :P_FURNACE";

            OracleCommand chkCmd = new OracleCommand(chkSql, con);
            chkCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
            chkCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;

            int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());

            if (cnt > 0)
            {
                // 3️⃣ UPDATE
                string updSql = @"
                    UPDATE Test.T_CAST_EXCEPTION
                    SET CAST_DATE =
                        TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,
                                'DD/MM/YYYY HH24:MI'),
                        HH24 = :P_HH,
                        MM   = :P_MM
                    WHERE ID_NO = :P_ID
                      AND FURNACE = :P_FURNACE";

                OracleCommand updCmd = new OracleCommand(updSql, con);
                updCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = castDate;
                updCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                updCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                updCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                updCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;

                updCmd.ExecuteNonQuery();
            }
            else
            {
                // 4️⃣ INSERT
                string insSql = @"
                    INSERT INTO Test.T_CAST_EXCEPTION
                    (ID_NO, FURNACE, CAST_DATE, HH24, MM)
                    VALUES
                    (:P_ID,
                     :P_FURNACE,
                     TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,
                             'DD/MM/YYYY HH24:MI'),
                     :P_HH,
                     :P_MM)";

                OracleCommand insCmd = new OracleCommand(insSql, con);
                insCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                insCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                insCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = castDate;
                insCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                insCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;

                insCmd.ExecuteNonQuery();
            }
        }
    }

    return Json("Insert / Update completed successfully");
}
