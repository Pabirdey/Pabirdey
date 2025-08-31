[HttpPost]
public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
{
    RmbbPile model = new RmbbPile();
    string message = "";
    bool recordFound = false;

    if (!string.IsNullOrEmpty(SaveRawMaterial))
    {
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            // Step 1: Calculate Weighted Averages from T_PSW_DAILY
            decimal? LD_Sludge_Cons = null, Mill_Scale_Cons = null, Flue_Dust_Cons = null, Esp_Dust_Cons = null,
                     Kiln_Dust_Cons = null, Gcp_Sludge_Cons = null, Lime_Fines_Cons = null, Wrp_MET_Cons = null,
                     LD_Slag_Fines_Cons = null, Mill_Sludge_Cons = null;

            string blendQuery = @"
                SELECT 
                    SUM(LD_Sludge), SUM(Mill_Scale), SUM(Flue_Dust), SUM(Esp_Dust),
                    SUM(Kiln_Dust), SUM(Gcp_Sludge), SUM(Lime_Fines), SUM(Wrp_MET),
                    SUM(LD_Slag_Fines), SUM(MILL_SLUDGE)
                FROM (
                    SELECT 
                        :vPSW1 * AVG(LD_Sludge) / 100 AS LD_Sludge,
                        :vPSW1 * AVG(Mill_Scale) / 100 AS Mill_Scale,
                        :vPSW1 * AVG(Flue_Dust) / 100 AS Flue_Dust,
                        :vPSW1 * AVG(Esp_Dust) / 100 AS Esp_Dust,
                        :vPSW1 * AVG(Kiln_Dust) / 100 AS Kiln_Dust,
                        :vPSW1 * AVG(Gcp_Sludge) / 100 AS Gcp_Sludge,
                        :vPSW1 * AVG(Lime_Fines) / 100 AS Lime_Fines,
                        :vPSW1 * AVG(WRP_MET) / 100 AS Wrp_MET,
                        :vPSW1 * AVG(LD_Slag_Fines) / 100 AS LD_Slag_Fines,
                        :vPSW1 * AVG(MILL_SLUDGE) / 100 AS MILL_SLUDGE
                    FROM T_PSW_DAILY
                    WHERE TRIM(SOURCE) = 'RMBB_KNR' AND TIMESTAMP >= TRUNC(:prepEndDate) - 200 AND BLEND_NO = :BL1

                    UNION

                    SELECT 
                        :vPSW2 * AVG(LD_Sludge) / 100 AS LD_Sludge,
                        :vPSW2 * AVG(Mill_Scale) / 100 AS Mill_Scale,
                        :vPSW2 * AVG(Flue_Dust) / 100 AS Flue_Dust,
                        :vPSW2 * AVG(Esp_Dust) / 100 AS Esp_Dust,
                        :vPSW2 * AVG(Kiln_Dust) / 100 AS Kiln_Dust,
                        :vPSW2 * AVG(Gcp_Sludge) / 100 AS Gcp_Sludge,
                        :vPSW2 * AVG(Lime_Fines) / 100 AS Lime_Fines,
                        :vPSW2 * AVG(WRP_MET) / 100 AS Wrp_MET,
                        :vPSW2 * AVG(LD_Slag_Fines) / 100 AS LD_Slag_Fines,
                        :vPSW2 * AVG(MILL_SLUDGE) / 100 AS MILL_SLUDGE
                    FROM T_PSW_DAILY
                    WHERE TRIM(SOURCE) = 'RMBB_KNR' AND TIMESTAMP >= TRUNC(:prepEndDate) - 200 AND BLEND_NO = :BL2
                )";

            using (OracleCommand blendCmd = new OracleCommand(blendQuery, conn))
            {
                blendCmd.Parameters.Add(":vPSW1", OracleDbType.Decimal).Value = input.PSW1 ?? 0;
                blendCmd.Parameters.Add(":prepEndDate", OracleDbType.Date).Value = input.EndDate ?? DateTime.Now;
                blendCmd.Parameters.Add(":BL1", OracleDbType.Int32).Value = input.BL1 ?? 0;

                blendCmd.Parameters.Add(":vPSW2", OracleDbType.Decimal).Value = input.PSW2 ?? 0;
                blendCmd.Parameters.Add(":BL2", OracleDbType.Int32).Value = input.BL2 ?? 0;

                using (OracleDataReader reader = blendCmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        LD_Sludge_Cons = reader.IsDBNull(0) ? null : reader.GetDecimal(0);
                        Mill_Scale_Cons = reader.IsDBNull(1) ? null : reader.GetDecimal(1);
                        Flue_Dust_Cons = reader.IsDBNull(2) ? null : reader.GetDecimal(2);
                        Esp_Dust_Cons = reader.IsDBNull(3) ? null : reader.GetDecimal(3);
                        Kiln_Dust_Cons = reader.IsDBNull(4) ? null : reader.GetDecimal(4);
                        Gcp_Sludge_Cons = reader.IsDBNull(5) ? null : reader.GetDecimal(5);
                        Lime_Fines_Cons = reader.IsDBNull(6) ? null : reader.GetDecimal(6);
                        Wrp_MET_Cons = reader.IsDBNull(7) ? null : reader.GetDecimal(7);
                        LD_Slag_Fines_Cons = reader.IsDBNull(8) ? null : reader.GetDecimal(8);
                        Mill_Sludge_Cons = reader.IsDBNull(9) ? null : reader.GetDecimal(9);
                    }
                }
            }

            // Step 2: Check if Record Exists
            string checkSql = "SELECT COUNT(*) FROM Test.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
            using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
            {
                int count = Convert.ToInt32(checkCmd.ExecuteScalar());
                if (count > 0)
                {
                    // Update
                    string updateSql = @"UPDATE Test.T_PILE_RAWMAT_QUANTITY_NEW SET                                         
                        PREP_START_DATE=:PREP_START_DATE,
                        PREP_END_DATE=:PREP_END_DATE,
                        CONS_ST_DATE=:CONS_ST_DATE,
                        NOA_FINES=:NOA_FINES,
                        JODA_FINES=:JODA_FINES,
                        KB_FINES=:KB_FINES
                        WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                    {
                        updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                        updateCmd.ExecuteNonQuery();
                        message = "Record Updated successfully!";
                    }
                }
                else
                {
                    // Insert
                    string insertSql = @"INSERT INTO Test.T_PILE_RAWMAT_QUANTITY_NEW
                    (PILE_NO, SOURCE, PREP_START_DATE, PREP_END_DATE, CONS_ST_DATE, NOA_FINES, JODA_FINES, KB_FINES)
                    VALUES (:PILE_NO, :SOURCE, :PREP_START_DATE, :PREP_END_DATE, :CONS_ST_DATE, :NOA_FINES, :JODA_FINES, :KB_FINES)";
                    using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                    {
                        insertCmd.Parameters.Add("PILE_NO", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                        insertCmd.Parameters.Add("SOURCE", OracleDbType.Varchar2).Value = input.Source ?? "";
                        insertCmd.Parameters.Add("PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add("PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add("CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add("NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add("JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add("KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                        insertCmd.ExecuteNonQuery();
                    }
                }
            }

            ViewBag.Message = "Data Saved Successfully!";
            model = input;
        }
    }
    else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();
            string query = "SELECT * FROM Test.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
            using (OracleCommand cmd = new OracleCommand(query, conn))
            {
                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        recordFound = true;
                        model.PileNo = input.PileNo;
                        model.Source = input.Source;
                        model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                        model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                        model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                        model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                        model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                        model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                    }
                }
            }
        }

        if (!recordFound)
        {
            ViewBag.Message = "No record exists for the given Pile No and Source.";
            model = new RmbbPile
            {
                PileNo = input.PileNo,
                Source = input.Source
            };
        }
    }

    return View(model);
}
   LD_Sludge_Cons = reader.IsDBNull(0) ? null : reader.GetDecimal(0);
                                Mill_Scale_Cons = reader.IsDBNull(1) ? null : reader.GetDecimal(1);
                                Flue_Dust_Cons = reader.IsDBNull(2) ? null : reader.GetDecimal(2);
                                Esp_Dust_Cons = reader.IsDBNull(3) ? null : reader.GetDecimal(3);
                                Kiln_Dust_Cons = reader.IsDBNull(4) ? null : reader.GetDecimal(4);
                                Gcp_Sludge_Cons = reader.IsDBNull(5) ? null : reader.GetDecimal(5);
                                Lime_Fines_Cons = reader.IsDBNull(6) ? null : reader.GetDecimal(6);
                                Wrp_MET_Cons = reader.IsDBNull(7) ? null : reader.GetDecimal(7);
                                LD_Slag_Fines_Cons = reader.IsDBNull(8) ? null : reader.GetDecimal(8);
                                Mill_Sludge_Cons = reader.IsDBNull(9) ? null : reader.GetDecimal(9);
