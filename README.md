[HttpPost]
public JsonResult SaveFurnaceCokeUnloading(Furnace_High_line model)
{
    using (OracleConnection con =
        new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        OracleTransaction trans = con.BeginTransaction();

        try
        {
            // =========================================
            // MAIN TABLE SAVE
            // =========================================

            foreach (var item in model.main)
            {
                if (string.IsNullOrWhiteSpace(item.Bunker))
                    continue;

                string query = @"

MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t

USING dual

ON
(
       t.TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY')
   AND t.SHIFT    = :SHIFT
   AND t.BUNKER   = :BUNKER
)

WHEN MATCHED THEN

UPDATE SET

    t.C               = :C,
    t.E               = :E,
    t.F               = :F,
    t.TOTAL           = :TOTAL,
    t.BUNKER_POSITION = :POSITION,
    t.BALANCE         = :BALANCE

WHEN NOT MATCHED THEN

INSERT
(
    TIMESTAMP,
    SHIFT,
    BUNKER,
    C,
    E,
    F,
    TOTAL,
    BUNKER_POSITION,
    BALANCE
)

VALUES
(
    TO_DATE(:TDATE,'DD/MM/YYYY'),
    :SHIFT,
    :BUNKER,
    :C,
    :E,
    :F,
    :TOTAL,
    :POSITION,
    :BALANCE
)

";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.BindByName = true;
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(":TDATE", item.Date);
                    cmd.Parameters.Add(":SHIFT", item.Shift);
                    cmd.Parameters.Add(":BUNKER", item.Bunker);

                    cmd.Parameters.Add(":C", item.C ?? "0");
                    cmd.Parameters.Add(":E", item.E ?? "0");
                    cmd.Parameters.Add(":F", item.F ?? "0");

                    cmd.Parameters.Add(":TOTAL", item.Total ?? "0");

                    cmd.Parameters.Add(":POSITION", item.Position ?? "0");
                    cmd.Parameters.Add(":BALANCE", item.Balance ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            // =========================================
            // COKE SAVE
            // =========================================

            foreach (var item in model.coke)
            {
                if (string.IsNullOrWhiteSpace(item.Bunker))
                    continue;

                string query = @"

MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t

USING dual

ON
(
       t.TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY')
   AND t.SHIFT    = :SHIFT
   AND t.BUNKER   = :BUNKER
)

WHEN MATCHED THEN

UPDATE SET

    t.TON_C_SC = :TON_C_SC,
    t.TON_E_SC = :TON_E_SC,
    t.TON_F_SC = :TON_F_SC

WHEN NOT MATCHED THEN

INSERT
(
    TIMESTAMP,
    SHIFT,
    BUNKER,
    TON_C_SC,
    TON_E_SC,
    TON_F_SC
)

VALUES
(
    TO_DATE(:TDATE,'DD/MM/YYYY'),
    :SHIFT,
    :BUNKER,
    :TON_C_SC,
    :TON_E_SC,
    :TON_F_SC
)

";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.BindByName = true;
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(":TDATE", item.Date);
                    cmd.Parameters.Add(":SHIFT", item.Shift);
                    cmd.Parameters.Add(":BUNKER", item.Bunker);

                    cmd.Parameters.Add(":TON_C_SC", item.C ?? "0");
                    cmd.Parameters.Add(":TON_E_SC", item.E ?? "0");
                    cmd.Parameters.Add(":TON_F_SC", item.F ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            // =========================================
            // NUT SAVE
            // =========================================

            foreach (var item in model.nut)
            {
                if (string.IsNullOrWhiteSpace(item.Bunker))
                    continue;

                string query = @"

MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t

USING dual

ON
(
       t.TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY')
   AND t.SHIFT    = :SHIFT
   AND t.BUNKER   = :BUNKER
)

WHEN MATCHED THEN

UPDATE SET

    t.TON_C_NC = :TON_C_NC,
    t.TON_E_NC = :TON_E_NC,
    t.TON_F_NC = :TON_F_NC

WHEN NOT MATCHED THEN

INSERT
(
    TIMESTAMP,
    SHIFT,
    BUNKER,
    TON_C_NC,
    TON_E_NC,
    TON_F_NC
)

VALUES
(
    TO_DATE(:TDATE,'DD/MM/YYYY'),
    :SHIFT,
    :BUNKER,
    :TON_C_NC,
    :TON_E_NC,
    :TON_F_NC
)

";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.BindByName = true;
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(":TDATE", item.Date);
                    cmd.Parameters.Add(":SHIFT", item.Shift);
                    cmd.Parameters.Add(":BUNKER", item.Bunker);

                    cmd.Parameters.Add(":TON_C_NC", item.C ?? "0");
                    cmd.Parameters.Add(":TON_E_NC", item.E ?? "0");
                    cmd.Parameters.Add(":TON_F_NC", item.F ?? "0");

                    cmd.ExecuteNonQuery();
                }
            }

            trans.Commit();

            return Json(new
            {
                success = true,
                message = "Data Saved Successfully"
            });
        }
        catch (Exception ex)
        {
            trans.Rollback();

            return Json(new
            {
                success = false,
                message = ex.Message
            });
        }
    }
}
