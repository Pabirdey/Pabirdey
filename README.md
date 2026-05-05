public JsonResult SaveFurnaceCokeUnloading(Furnace_High_line model)
{
    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();
        OracleTransaction trans = con.BeginTransaction();

        try
        {
            //--------------------------------------------
            // MAIN TABLE SAVE
            //--------------------------------------------
            foreach (var item in model.main)
            {
                string checkQuery = @"
                    SELECT COUNT(*)
                    FROM imtg.T_BF_CK_CONTROL_UNLOADING
                    WHERE TRUNC(""TIMESTAMP"") = TO_DATE(:p_date,'DD/MM/YYYY')
                    AND SHIFT = :p_shift
                    AND BUNKER = :p_bunker";

                int count = 0;

                using (OracleCommand checkCmd = new OracleCommand(checkQuery, con))
                {
                    checkCmd.Transaction = trans;
                    checkCmd.BindByName = true;

                    checkCmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = item.Date;
                    checkCmd.Parameters.Add("p_shift", OracleDbType.Varchar2).Value = item.Shift;
                    checkCmd.Parameters.Add("p_bunker", OracleDbType.Varchar2).Value = item.Bunker;

                    count = Convert.ToInt32(checkCmd.ExecuteScalar());
                }

                string query = "";

                if (count > 0)
                {
                    query = @"
                        UPDATE imtg.T_BF_CK_CONTROL_UNLOADING
                        SET 
                            C_BF = :p_c,
                            E_BF = :p_e,
                            F_BF = :p_f,
                            TOTAL = :p_total,
                            BUNKER_POSITION = :p_position,
                            BALANCE = :p_balance
                        WHERE TRUNC(""TIMESTAMP"") = TO_DATE(:p_date,'DD/MM/YYYY')
                        AND SHIFT = :p_shift
                        AND BUNKER = :p_bunker";
                }
                else
                {
                    query = @"
                        INSERT INTO imtg.T_BF_CK_CONTROL_UNLOADING
                        (
                            TIMESTAMP,
                            SHIFT,
                            BUNKER,
                            C_BF,
                            E_BF,
                            F_BF,
                            TOTAL,
                            BUNKER_POSITION,
                            BALANCE
                        )
                        VALUES
                        (
                            TO_DATE(:p_date,'DD/MM/YYYY'),
                            :p_shift,
                            :p_bunker,
                            :p_c,
                            :p_e,
                            :p_f,
                            :p_total,
                            :p_position,
                            :p_balance
                        )";
                }

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;
                    cmd.BindByName = true;

                    cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = item.Date;
                    cmd.Parameters.Add("p_shift", OracleDbType.Varchar2).Value = item.Shift;
                    cmd.Parameters.Add("p_bunker", OracleDbType.Varchar2).Value = item.Bunker;

                    cmd.Parameters.Add("p_c", OracleDbType.Varchar2).Value = item.C ?? "";
                    cmd.Parameters.Add("p_e", OracleDbType.Varchar2).Value = item.E ?? "";
                    cmd.Parameters.Add("p_f", OracleDbType.Varchar2).Value = item.F ?? "";
                    cmd.Parameters.Add("p_total", OracleDbType.Varchar2).Value = item.Total ?? "";

                    cmd.Parameters.Add("p_position", OracleDbType.Varchar2).Value = item.Position ?? "";
                    cmd.Parameters.Add("p_balance", OracleDbType.Varchar2).Value = item.Balance ?? "";

                    cmd.ExecuteNonQuery();
                }
            }

            //--------------------------------------------
            // COKE SAVE
            //--------------------------------------------
            foreach (var item in model.coke)
            {
                string query = @"
                    UPDATE imtg.T_BF_CK_CONTROL_UNLOADING
                    SET
                        TON_C_SC = :p_c,
                        TON_E_SC = :p_e,
                        TON_F_SC = :p_f
                    WHERE TRUNC(""TIMESTAMP"") = TO_DATE(:p_date,'DD/MM/YYYY')
                    AND SHIFT = :p_shift
                    AND BUNKER = :p_bunker";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;
                    cmd.BindByName = true;

                    cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = item.Date;
                    cmd.Parameters.Add("p_shift", OracleDbType.Varchar2).Value = item.Shift;
                    cmd.Parameters.Add("p_bunker", OracleDbType.Varchar2).Value = item.Bunker;

                    cmd.Parameters.Add("p_c", OracleDbType.Varchar2).Value = item.C ?? "";
                    cmd.Parameters.Add("p_e", OracleDbType.Varchar2).Value = item.E ?? "";
                    cmd.Parameters.Add("p_f", OracleDbType.Varchar2).Value = item.F ?? "";

                    cmd.ExecuteNonQuery();
                }
            }

            //--------------------------------------------
            // NUT SAVE
            //--------------------------------------------
            foreach (var item in model.nut)
            {
                string query = @"
                    UPDATE imtg.T_BF_CK_CONTROL_UNLOADING
                    SET
                        TON_C_NC = :p_c,
                        TON_E_NC = :p_e,
                        TON_F_NC = :p_f
                    WHERE TRUNC(""TIMESTAMP"") = TO_DATE(:p_date,'DD/MM/YYYY')
                    AND SHIFT = :p_shift
                    AND BUNKER = :p_bunker";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;
                    cmd.BindByName = true;

                    cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = item.Date;
                    cmd.Parameters.Add("p_shift", OracleDbType.Varchar2).Value = item.Shift;
                    cmd.Parameters.Add("p_bunker", OracleDbType.Varchar2).Value = item.Bunker;

                    cmd.Parameters.Add("p_c", OracleDbType.Varchar2).Value = item.C ?? "";
                    cmd.Parameters.Add("p_e", OracleDbType.Varchar2).Value = item.E ?? "";
                    cmd.Parameters.Add("p_f", OracleDbType.Varchar2).Value = item.F ?? "";

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
