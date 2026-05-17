[HttpPost]
public JsonResult SaveBFProdData(List<BFViewModel> modelList)
{
    try
    {
        using (OracleConnection con =
            new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            for (int i = 0; i < modelList.Count; i++)
            {
                BFViewModel model = modelList[i];

                // ===== CHECK RECORD EXISTS =====

                string checkQuery = @"
                SELECT COUNT(*)
                FROM TEST.T_BF_PRODUCTION_TRACKING
                WHERE FURNACE = :FURNACE
                AND TIMESTAMP = :TIMESTAMP";

                int count = 0;

                using (OracleCommand cmd =
                    new OracleCommand(checkQuery, con))
                {
                    cmd.BindByName = true;

                    cmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value =
                        model.FURNACE;

                    cmd.Parameters.Add("TIMESTAMP",
                        OracleDbType.Date).Value =
                        Convert.ToDateTime(model.PROD_DATE);

                    count = Convert.ToInt32(cmd.ExecuteScalar());
                }

                // ===== UPDATE =====

                if (count > 0)
                {
                    string updateQuery = @"

                    UPDATE TEST.T_BF_PRODUCTION_TRACKING

                    SET

                        ACTUAL = :ACTUAL,
                        REPORTED = :REPORTED,
                        BALANCE = :BALANCE

                    WHERE

                        FURNACE = :FURNACE
                        AND TIMESTAMP = :TIMESTAMP";

                    using (OracleCommand cmd =
                        new OracleCommand(updateQuery, con))
                    {
                        cmd.BindByName = true;

                        cmd.Parameters.Add("ACTUAL",
                            OracleDbType.Decimal).Value =
                            model.ACTUAL;

                        cmd.Parameters.Add("REPORTED",
                            OracleDbType.Decimal).Value =
                            model.REPORTED;

                        cmd.Parameters.Add("BALANCE",
                            OracleDbType.Decimal).Value =
                            model.BALANCE;

                        cmd.Parameters.Add("FURNACE",
                            OracleDbType.Varchar2).Value =
                            model.FURNACE;

                        cmd.Parameters.Add("TIMESTAMP",
                            OracleDbType.Date).Value =
                            Convert.ToDateTime(model.PROD_DATE);

                        cmd.ExecuteNonQuery();
                    }
                }

                // ===== INSERT =====

                else
                {
                    string insertQuery = @"

                    INSERT INTO TEST.T_BF_PRODUCTION_TRACKING
                    (
                        FURNACE,
                        TIMESTAMP,
                        ACTUAL,
                        REPORTED,
                        BALANCE
                    )

                    VALUES
                    (
                        :FURNACE,
                        :TIMESTAMP,
                        :ACTUAL,
                        :REPORTED,
                        :BALANCE
                    )";

                    using (OracleCommand cmd =
                        new OracleCommand(insertQuery, con))
                    {
                        cmd.BindByName = true;

                        cmd.Parameters.Add("FURNACE",
                            OracleDbType.Varchar2).Value =
                            model.FURNACE;

                        cmd.Parameters.Add("TIMESTAMP",
                            OracleDbType.Date).Value =
                            Convert.ToDateTime(model.PROD_DATE);

                        cmd.Parameters.Add("ACTUAL",
                            OracleDbType.Decimal).Value =
                            model.ACTUAL;

                        cmd.Parameters.Add("REPORTED",
                            OracleDbType.Decimal).Value =
                            model.REPORTED;

                        cmd.Parameters.Add("BALANCE",
                            OracleDbType.Decimal).Value =
                            model.BALANCE;

                        cmd.ExecuteNonQuery();
                    }
                }
            }
        }

        return Json(new
        {
            success = true,
            message = "Data Saved Successfully"
        });
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
