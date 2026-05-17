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

                string query = @"

                MERGE INTO TEST.T_BF_PRODUCTION t

                USING
                (
                    SELECT
                        :FURNACE AS FURNACE,
                        :PROD_DATE AS PROD_DATE
                    FROM dual
                ) s

                ON
                (
                    t.FURNACE = s.FURNACE
                    AND t.PROD_DATE = s.PROD_DATE
                )

                WHEN MATCHED THEN

                    UPDATE SET

                        ACTUAL         = :ACTUAL,
                        ACTUAL_TD      = :ACTUAL_TD,

                        REPORTED       = :REPORTED,
                        REPORTED_TD    = :REPORTED_TD,

                        BALANCE        = :BALANCE

                WHEN NOT MATCHED THEN

                    INSERT
                    (
                        FURNACE,
                        PROD_DATE,

                        ACTUAL,
                        ACTUAL_TD,

                        REPORTED,
                        REPORTED_TD,

                        BALANCE
                    )

                    VALUES
                    (
                        :FURNACE,
                        :PROD_DATE,

                        :ACTUAL,
                        :ACTUAL_TD,

                        :REPORTED,
                        :REPORTED_TD,

                        :BALANCE
                    )";

                using (OracleCommand cmd =
                    new OracleCommand(query, con))
                {
                    cmd.BindByName = true;

                    cmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value =
                        model.FURNACE;

                    cmd.Parameters.Add("PROD_DATE",
                        OracleDbType.Date).Value =
                        Convert.ToDateTime(model.PROD_DATE);

                    cmd.Parameters.Add("ACTUAL",
                        OracleDbType.Decimal).Value =
                        model.ACTUAL;

                    cmd.Parameters.Add("ACTUAL_TD",
                        OracleDbType.Decimal).Value =
                        model.ACTUAL_TD;

                    cmd.Parameters.Add("REPORTED",
                        OracleDbType.Decimal).Value =
                        model.REPORTED;

                    cmd.Parameters.Add("REPORTED_TD",
                        OracleDbType.Decimal).Value =
                        model.REPORTED_TD;

                    cmd.Parameters.Add("BALANCE",
                        OracleDbType.Decimal).Value =
                        model.BALANCE;

                    cmd.ExecuteNonQuery();
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
