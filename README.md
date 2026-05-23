 foreach (var item in model.coke)
            {
                if (string.IsNullOrWhiteSpace(item.Bunker))
                    continue;

                string query = @"UPDATE test.T_BF_CK_CONTROL_UNLOADING
                                SET
                                    TON_C_SC = :TON_C_SC,
                                    TON_E_SC = :TON_E_SC,
                                    TON_F_SC = :TON_F_SC
                                WHERE
                                    TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY')
                                    AND SHIFT = :SHIFT
                                    AND BUNKER = :BUNKER";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;
                    cmd.BindByName = true;

                    cmd.Parameters.Add(":TON_C_SC", item.C ?? "0");
                    cmd.Parameters.Add(":TON_E_SC", item.E ?? "0");
                    cmd.Parameters.Add(":TON_F_SC", item.F ?? "0");

                    cmd.Parameters.Add(":TDATE", item.Date);
                    cmd.Parameters.Add(":SHIFT", item.Shift);
                    cmd.Parameters.Add(":BUNKER", item.Bunker);

                    cmd.ExecuteNonQuery();
                }
            }

            // =========================
            // NUT UPDATE
            // =========================
            foreach (var item in model.nut)
            {
                if (string.IsNullOrWhiteSpace(item.Bunker))
                    continue;

                string query = @"UPDATE test.T_BF_CK_CONTROL_UNLOADING
                                SET
                                    TON_C_NC = :TON_C_NC,
                                    TON_E_NC = :TON_E_NC,
                                    TON_F_NC = :TON_F_NC
                                WHERE
                                    TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY')
                                    AND SHIFT = :SHIFT
                                    AND BUNKER = :BUNKER";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;
                    cmd.BindByName = true;

                    cmd.Parameters.Add(":TON_C_NC", item.C ?? "0");
                    cmd.Parameters.Add(":TON_E_NC", item.E ?? "0");
                    cmd.Parameters.Add(":TON_F_NC", item.F ?? "0");

                    cmd.Parameters.Add(":TDATE", item.Date);
                    cmd.Parameters.Add(":SHIFT", item.Shift);
                    cmd.Parameters.Add(":BUNKER", item.Bunker);

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
