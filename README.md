[HttpPost]
public JsonResult Save_Exception_Cast(List<object> data)
{
    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        foreach (var item in data)
        {
            var row = item as Newtonsoft.Json.Linq.JObject; // convert dynamic object to JObject

            string idNo = row?["ID_NO"]?.ToString();
            string tapholeno = row?["TAPHOLE_NO"]?.ToString();
            string furnace = row?["FURNACE"]?.ToString();
            string exceptiondate = row?["EXCEPTION_DATE"]?.ToString();
            string hh24 = row?["HH24"]?.ToString() ?? "00";
            string mm = row?["MM"]?.ToString() ?? "00";
            string tapholelength = row?["TAPHOLE_LENGTH"]?.ToString();
            string claypaused = row?["CLAY_PAUSED"]?.ToString();
            string type = row?["TYPE"]?.ToString();

            // skip if ID or Date is null
            if (string.IsNullOrEmpty(idNo) || string.IsNullOrEmpty(exceptiondate))
                continue;

            // Check if record exists
            string chkSql = @"SELECT COUNT(1) 
                              FROM Test.T_CAST_EXCEPTION 
                              WHERE ID_NO = :P_ID AND FUR_NAME = :P_FURNACE";

            OracleCommand chkCmd = new OracleCommand(chkSql, con);
            chkCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
            chkCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace ?? "";
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
                updCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptiondate;
                updCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                updCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                updCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapholelength ?? "";
                updCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = claypaused ?? "";
                updCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type ?? "";
                updCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeno ?? "";
                updCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                updCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace ?? "";
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
                insCmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptiondate;
                insCmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                insCmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                insCmd.Parameters.Add("P_TAPHOLELENGTH", OracleDbType.Varchar2).Value = tapholelength ?? "";
                insCmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = claypaused ?? "";
                insCmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type ?? "";
                insCmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeno ?? "";
                insCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                insCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace ?? "";
                insCmd.ExecuteNonQuery();
            }
        }
    }

    return Json("Insert / Update completed successfully");
}
