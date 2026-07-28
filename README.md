[HttpPost]
public JsonResult SaveLadleData(LadleModel model)
{
    try
    {
        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            // Check record exists
            string checkQuery = @"SELECT COUNT(*) 
                                  FROM DEMO.T_LADLE
                                  WHERE DATE_TIME = :P_DATE
                                  AND PLANT = 'G'";

            int vCount = 0;

            using (OracleCommand cmd = new OracleCommand(checkQuery, con))
            {
                cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = model.DATE_TIME_PROD_F;

                vCount = Convert.ToInt32(cmd.ExecuteScalar());
            }

            if (vCount > 0)
            {
                // Update
                string updateQuery = @"
                    UPDATE DEMO.T_LADLE
                    SET DATE_TIME = :P_NEW_DATE,
                        LD1_TONS = NULL,
                        LD2_TONS = NULL,
                        LD3_TONS = NULL,
                        MRDTP_TONS = NULL,
                        NOOFTP = :P_NOOFTP
                    WHERE DATE_TIME = :P_OLD_DATE
                    AND PLANT = 'G'";

                using (OracleCommand cmd = new OracleCommand(updateQuery, con))
                {
                    cmd.Parameters.Add(":P_NEW_DATE", OracleDbType.Date).Value = model.DATE_TIME;
                    cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Int32).Value = model.NOOFTP_G;
                    cmd.Parameters.Add(":P_OLD_DATE", OracleDbType.Date).Value = model.DATE_TIME_PROD_F;

                    cmd.ExecuteNonQuery();
                }
            }
            else
            {
                // Insert
                string insertQuery = @"
                    INSERT INTO DEMO.T_LADLE
                    (
                        DATE_TIME,
                        LD1_TONS,
                        LD2_TONS,
                        LD3_TONS,
                        MRDTP_TONS,
                        NOOFTP,
                        LD1_TONS_ACTUAL,
                        LD2_TONS_ACTUAL,
                        LD3_TONS_ACTUAL,
                        MRDTP_TONS_ACTUAL,
                        PLANT
                    )
                    VALUES
                    (
                        :P_DATE,
                        NULL,
                        NULL,
                        NULL,
                        NULL,
                        :P_NOOFTP,
                        :P_LD1_ACTUAL,
                        :P_LD2_ACTUAL,
                        :P_LD3_ACTUAL,
                        :P_MRDTP_ACTUAL,
                        'G'
                    )";

                using (OracleCommand cmd = new OracleCommand(insertQuery, con))
                {
                    cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = model.DATE_TIME;
                    cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Int32).Value = model.NOOFTP_G;
                    cmd.Parameters.Add(":P_LD1_ACTUAL", OracleDbType.Decimal).Value = model.LD1_TONS_ACTUAL_G;
                    cmd.Parameters.Add(":P_LD2_ACTUAL", OracleDbType.Decimal).Value = model.LD2_TONS_ACTUAL_G;
                    cmd.Parameters.Add(":P_LD3_ACTUAL", OracleDbType.Decimal).Value = model.LD3_TONS_ACTUAL_G;
                    cmd.Parameters.Add(":P_MRDTP_ACTUAL", OracleDbType.Decimal).Value = model.MRDTP_TONS_ACTUAL_G;

                    cmd.ExecuteNonQuery();
                }
            }

            return Json(new
            {
                success = true,
                message = "Data saved successfully."
            });
        }
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        });
    }
}
