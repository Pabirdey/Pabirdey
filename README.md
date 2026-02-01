[HttpPost]
        public JsonResult Save_Exception_Cast(List<Dictionary<string, string>> data)
        {
            if (data == null || data.Count == 0)
                return Json("No data received");

            using (OracleConnection con =
                   new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                foreach (var row in data)
                {
                    string idNo = row["ID_NO"];
                    string furnace = row["FURNACE"];
                    string tapholeNo = row["TAPHOLE_NO"];
                    string exceptionDate = row["EXCEPTION_DATE"];
                    string hh24 = row["HH24"];
                    string mm = row["MM"];
                    string tapLength = row["TAPHOLE_LENGTH"];
                    string clayPaused = row["CLAY_PAUSED"];
                    string type = row["TYPE"];

                    // Mandatory check
                    if (string.IsNullOrWhiteSpace(idNo) ||
                        string.IsNullOrWhiteSpace(exceptionDate))
                        continue;

                    // CHECK
                    OracleCommand chkCmd = new OracleCommand(@"
                SELECT COUNT(1)
                FROM Test.T_CAST_EXCEPTION
                WHERE ID_NO = :P_ID
                  AND FUR_NAME = :P_FURNACE", con);

                    chkCmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                    chkCmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;

                    int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());

                    OracleCommand cmd = new OracleCommand();
                    cmd.Connection = con;

                    if (cnt > 0)
                    {
                        cmd.CommandText = @"
                    UPDATE Test.T_CAST_EXCEPTION
                    SET DATE_TIME = TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,
                                            'DD/MM/YYYY HH24:MI'),
                        TAPHOLE_LENGTH = :P_TAPLEN,
                        CLAY_PUSHED = :P_CLAY,
                        TYPE = :P_TYPE,
                        TAPHOLE_NO = :P_TAPHOLENO                      
                    WHERE ID_NO = :P_ID
                      AND FUR_NAME = :P_FURNACE";
                    }
                    else
                    {
                        cmd.CommandText = @"
                    INSERT INTO Test.T_CAST_EXCEPTION
                    (DATE_TIME, FUR_NAME, ID_NO,
                     TAPHOLE_LENGTH, CLAY_PUSHED, TYPE,
                     TAPHOLE_NO, HH24, MM)
                    VALUES
                    (TO_DATE(:P_DATE || ' ' || :P_HH || ':' || :P_MM,
                             'DD/MM/YYYY HH24:MI'),
                     :P_FURNACE, :P_ID,
                     :P_TAPLEN, :P_CLAY, :P_TYPE,
                     :P_TAPHOLENO, :P_HH, :P_MM)";
                    }

                    cmd.Parameters.Add("P_DATE", OracleDbType.Varchar2).Value = exceptionDate;
                    cmd.Parameters.Add("P_HH", OracleDbType.Varchar2).Value = hh24;
                    cmd.Parameters.Add("P_MM", OracleDbType.Varchar2).Value = mm;
                    cmd.Parameters.Add("P_TAPLEN", OracleDbType.Varchar2).Value = tapLength;
                    cmd.Parameters.Add("P_CLAY", OracleDbType.Varchar2).Value = clayPaused;
                    cmd.Parameters.Add("P_TYPE", OracleDbType.Varchar2).Value = type;
                    cmd.Parameters.Add("P_TAPHOLENO", OracleDbType.Varchar2).Value = tapholeNo;
                    cmd.Parameters.Add("P_ID", OracleDbType.Varchar2).Value = idNo;
                    cmd.Parameters.Add("P_FURNACE", OracleDbType.Varchar2).Value = furnace;

                    cmd.ExecuteNonQuery();
                }
            }

            return Json("Insert / Update completed successfully");
        }
