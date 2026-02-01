[HttpPost]
public JsonResult Save_Exception_Cast(List<dynamic> data)
{
    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        foreach (var row in data)
        {
            string idNo = Convert.ToString(row.ID_NO);
            string furnace = Convert.ToString(row.FURNACE);
            string date = Convert.ToString(row.EXCEPTION_DATE);
            string hh = Convert.ToString(row.HH24);
            string mm = Convert.ToString(row.MM);
            string tapLen = Convert.ToString(row.TAPHOLE_LENGTH);
            string clay = Convert.ToString(row.CLAY_PAUSED);
            string type = Convert.ToString(row.TYPE);
            string tapholeNo = Convert.ToString(row.TAPHOLE_NO);

            // Skip row if ID or Date is null
            if (string.IsNullOrEmpty(idNo) || string.IsNullOrEmpty(date)) continue;

            // Check if record exists
            string chkSql = @"SELECT COUNT(1) FROM Test.T_CAST_EXCEPTION 
                              WHERE ID_NO=:P_ID AND FUR_NAME=:P_FURNACE";
            OracleCommand chkCmd = new OracleCommand(chkSql, con);
            chkCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
            chkCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
            int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());

            if (cnt > 0)
            {
                // UPDATE
                string updSql = @"
                    UPDATE Test.T_CAST_EXCEPTION
                    SET DATE_TIME = TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,'DD/MM/YYYY HH24:MI'),
                        TAPHOLE_LENGTH = :P_TAPHOLELENGTH,
                        CLAY_PUSHED = :P_CLAY,
                        TYPE = :P_TYPE,
                        TAPHOLE_NO = :P_TAPHOLENO,
                        HH24 = :P_HH,
                        MM = :P_MM
                    WHERE ID_NO = :P_ID
                      AND FUR_NAME = :P_FURNACE";

                OracleCommand updCmd = new OracleCommand(updSql, con);
                updCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = date;
                updCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh;
                updCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                updCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapLen;
                updCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = clay;
                updCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type;
                updCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeNo;
                updCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                updCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                updCmd.ExecuteNonQuery();
            }
            else
            {
                // INSERT
                string insSql = @"
                    INSERT INTO Test.T_CAST_EXCEPTION
                    (DATE_TIME, FUR_NAME, ID_NO, TAPHOLE_LENGTH, CLAY_PUSHED, TYPE, TAPHOLE_NO, HH24, MM)
                    VALUES
                    (TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,'DD/MM/YYYY HH24:MI'),
                     :P_FURNACE, :P_ID, :P_TAPHOLELENGTH, :P_CLAY, :P_TYPE, :P_TAPHOLENO, :P_HH, :P_MM)";

                OracleCommand insCmd = new OracleCommand(insSql, con);
                insCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = date;
                insCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh;
                insCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                insCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapLen;
                insCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = clay;
                insCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type;
                insCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeNo;
                insCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                insCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;
                insCmd.ExecuteNonQuery();
            }
        }
    }

    return Json("Insert / Update completed successfully");
}
