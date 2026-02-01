[HttpPost]
public JsonResult Save_Exception_Cast(List<dynamic> data)
{
    using (OracleConnection con = new OracleConnection(connectionString))
    {
        con.Open();

        for (int i = 0; i < data.Count; i++)
        {
            // 1️⃣ Get current row values
            string idNo = data[i].ID_NO;
            string castDate = data[i].CAST_DATE;

            // 2️⃣ Skip row if ID or Date is empty/null
            if (string.IsNullOrEmpty(idNo) || string.IsNullOrEmpty(castDate))
            {
                // Optional: log skipped row or ignore silently
                continue; // skip to next row
            }

            // 3️⃣ Check record exists
            string chkSql = "SELECT COUNT(1) FROM T_EXCEPTION_CAST WHERE ID_NO = :ID_NO";

            OracleCommand chkCmd = new OracleCommand(chkSql, con);
            chkCmd.Parameters.Add(":ID_NO", idNo);

            int cnt = Convert.ToInt32(chkCmd.ExecuteScalar());

            if (cnt > 0)
            {
                // 4️⃣ UPDATE existing row
                string updSql = @"
                    UPDATE T_EXCEPTION_CAST
                    SET CAST_DATE = TO_DATE(:CAST_DATE,'DD/MM/YYYY'),
                        HH24 = :HH24,
                        MM   = :MM
                    WHERE ID_NO = :ID_NO";

                OracleCommand updCmd = new OracleCommand(updSql, con);
                updCmd.Parameters.Add(":CAST_DATE", castDate);
                updCmd.Parameters.Add(":HH24", data[i].HH24);
                updCmd.Parameters.Add(":MM", data[i].MM);
                updCmd.Parameters.Add(":ID_NO", idNo);

                updCmd.ExecuteNonQuery();
            }
            else
            {
                // 5️⃣ INSERT new row
                string insSql = @"
                    INSERT INTO T_EXCEPTION_CAST
                    (ID_NO, CAST_DATE, HH24, MM)
                    VALUES
                    (:ID_NO, TO_DATE(:CAST_DATE,'DD/MM/YYYY'), :HH24, :MM)";

                OracleCommand insCmd = new OracleCommand(insSql, con);
                insCmd.Parameters.Add(":ID_NO", idNo);
                insCmd.Parameters.Add(":CAST_DATE", castDate);
                insCmd.Parameters.Add(":HH24", data[i].HH24);
                insCmd.Parameters.Add(":MM", data[i].MM);

                insCmd.ExecuteNonQuery();
            }
        }
    }

    return Json("Insert / Update completed successfully");
}