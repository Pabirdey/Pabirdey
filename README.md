[HttpPost]
public JsonResult SaveDrillSlagSourceWise(List<Dictionary<string, string>> data)
{
    string conStr = ConfigurationManager.ConnectionStrings["OracleCon"].ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        foreach (var row in data)
        {
            // 1. Try to UPDATE
            string updateSql = @"UPDATE CAST_HOUSE_DRILL SET 
                                    DRILL_DIA = :1, 
                                    DRILL_TYPE = :2, 
                                    DRILL_TIME = :3,
                                    BARS = :4,
                                    SLAG_START = :5, 
                                    SLAG_RATIO = :6, 
                                    GRANULATION = :7
                                 WHERE CAST_NO = :8";

            using (OracleCommand updateCmd = new OracleCommand(updateSql, con))
            {
                updateCmd.Parameters.Add(new OracleParameter("1", row["DrillDia"]));
                updateCmd.Parameters.Add(new OracleParameter("2", row["DrillType"]));
                updateCmd.Parameters.Add(new OracleParameter("3", row["DrillTime"]));
                updateCmd.Parameters.Add(new OracleParameter("4", row["Bars"]));
                updateCmd.Parameters.Add(new OracleParameter("5", row["SlagStart"]));
                updateCmd.Parameters.Add(new OracleParameter("6", row["SlagRatio"]));
                updateCmd.Parameters.Add(new OracleParameter("7", row["Granulation"]));
                updateCmd.Parameters.Add(new OracleParameter("8", row["CastNo"]));

                int rowsUpdated = updateCmd.ExecuteNonQuery();

                // 2. If no row updated, do INSERT
                if (rowsUpdated == 0)
                {
                    string insertSql = @"INSERT INTO CAST_HOUSE_DRILL 
                                        (CAST_NO, DRILL_DIA, DRILL_TYPE, DRILL_TIME, BARS, SLAG_START, SLAG_RATIO, GRANULATION)
                                        VALUES (:1, :2, :3, :4, :5, :6, :7, :8)";
                    using (OracleCommand insertCmd = new OracleCommand(insertSql, con))
                    {
                        insertCmd.Parameters.Add(new OracleParameter("1", row["CastNo"]));
                        insertCmd.Parameters.Add(new OracleParameter("2", row["DrillDia"]));
                        insertCmd.Parameters.Add(new OracleParameter("3", row["DrillType"]));
                        insertCmd.Parameters.Add(new OracleParameter("4", row["DrillTime"]));
                        insertCmd.Parameters.Add(new OracleParameter("5", row["Bars"]));
                        insertCmd.Parameters.Add(new OracleParameter("6", row["SlagStart"]));
                        insertCmd.Parameters.Add(new OracleParameter("7", row["SlagRatio"]));
                        insertCmd.Parameters.Add(new OracleParameter("8", row["Granulation"]));
                        insertCmd.ExecuteNonQuery();
                    }
                }
            }
        }
    }

    return Json("Success");
}
