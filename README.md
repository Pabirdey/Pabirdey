[HttpPost]
public JsonResult SaveAllData(
    List<BFViewModel> modelList,
    LadleModel model)
{
    string conString = ConfigurationManager
        .ConnectionStrings["OracleDBConnection"]
        .ConnectionString;

    using (OracleConnection con =
        new OracleConnection(conString))
    {
        con.Open();

        OracleTransaction trans =
            con.BeginTransaction();

        try
        {
            #region BF PRODUCTION TRACKING

            for (int i = 0; i < modelList.Count; i++)
            {
                BFViewModel bfModel = modelList[i];

                string checkQuery = @"

                    SELECT COUNT(*)

                    FROM DEMO.T_BF_PRODUCTION_TRACKING

                    WHERE FURNACE = :FURNACE
                    AND TIMESTAMP = :TIMESTAMP";

                int count = 0;

                using (OracleCommand cmd =
                    new OracleCommand(checkQuery, con))
                {
                    cmd.Transaction = trans;

                    cmd.BindByName = true;

                    cmd.Parameters.Add("FURNACE",
                        OracleDbType.Varchar2).Value =
                        bfModel.FURNACE;

                    cmd.Parameters.Add("TIMESTAMP",
                        OracleDbType.Date).Value =
                        Convert.ToDateTime(
                            bfModel.PROD_DATE);

                    count = Convert.ToInt32(
                        cmd.ExecuteScalar());
                }

                if (count > 0)
                {
                    string updateQuery = @"

                        UPDATE DEMO.T_BF_PRODUCTION_TRACKING

                        SET
                            ACTUAL = :ACTUAL,
                            REPORTED = :REPORTED,
                            BALANCE = :BALANCE

                        WHERE FURNACE = :FURNACE
                        AND TIMESTAMP = :TIMESTAMP";

                    using (OracleCommand cmd =
                        new OracleCommand(updateQuery, con))
                    {
                        cmd.Transaction = trans;

                        cmd.BindByName = true;

                        cmd.Parameters.Add("ACTUAL",
                            OracleDbType.Decimal).Value =
                            bfModel.ACTUAL;

                        cmd.Parameters.Add("REPORTED",
                            OracleDbType.Decimal).Value =
                            bfModel.REPORTED;

                        cmd.Parameters.Add("BALANCE",
                            OracleDbType.Decimal).Value =
                            bfModel.BALANCE;

                        cmd.Parameters.Add("FURNACE",
                            OracleDbType.Varchar2).Value =
                            bfModel.FURNACE;

                        cmd.Parameters.Add("TIMESTAMP",
                            OracleDbType.Date).Value =
                            Convert.ToDateTime(
                                bfModel.PROD_DATE);

                        cmd.ExecuteNonQuery();
                    }
                }
                else
                {
                    string insertQuery = @"

                        INSERT INTO DEMO.T_BF_PRODUCTION_TRACKING
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
                        cmd.Transaction = trans;

                        cmd.BindByName = true;

                        cmd.Parameters.Add("FURNACE",
                            OracleDbType.Varchar2).Value =
                            bfModel.FURNACE;

                        cmd.Parameters.Add("TIMESTAMP",
                            OracleDbType.Date).Value =
                            Convert.ToDateTime(
                                bfModel.PROD_DATE);

                        cmd.Parameters.Add("ACTUAL",
                            OracleDbType.Decimal).Value =
                            bfModel.ACTUAL;

                        cmd.Parameters.Add("REPORTED",
                            OracleDbType.Decimal).Value =
                            bfModel.REPORTED;

                        cmd.Parameters.Add("BALANCE",
                            OracleDbType.Decimal).Value =
                            bfModel.BALANCE;

                        cmd.ExecuteNonQuery();
                    }
                }
            }

            #endregion

            decimal? vTotalTP = null;
            decimal? vTotalOT = null;

            decimal? vTotProdTP = null;
            decimal? vTotProdOT = null;

            decimal? vHMT_TP = null;
            decimal? vHMT_OT = null;

            #region A-F PLANT

            int VCount = 0;

            string countQry = @"

                SELECT COUNT(*)

                FROM DEMO.T_LADLE

                WHERE DATE_TIME =
                      TO_DATE(:DATE_TIME_PROD_F,
                      'DD-MM-YYYY HH24:MI:SS')

                AND PLANT='A-F'";

            using (OracleCommand cmd =
                new OracleCommand(countQry, con))
            {
                cmd.Transaction = trans;

                cmd.Parameters.Add(
                    "DATE_TIME_PROD_F",
                    OracleDbType.Varchar2).Value =
                    model.DATE_TIME_PROD_F;

                VCount = Convert.ToInt32(
                    cmd.ExecuteScalar());
            }

            if (VCount > 0)
            {
                string updateQry = @"

                    UPDATE DEMO.T_LADLE

                    SET
                        DATE_TIME =
                        TO_DATE(:DATE_TIME,
                        'DD-MM-YYYY HH24:MI:SS'),

                        LD1_TONS = :LD1_TONS,
                        LD2_TONS = :LD2_TONS,
                        LD3_TONS = :LD3_TONS,

                        MRDTP_TONS = :MRDTP_TONS,

                        NOOFTP = :NOOFTP

                    WHERE DATE_TIME =
                          TO_DATE(:DATE_TIME_PROD_F,
                          'DD-MM-YYYY HH24:MI:SS')

                    AND PLANT='A-F'";

                using (OracleCommand cmd =
                    new OracleCommand(updateQry, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    cmd.Parameters.Add(
                        "LD1_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD1_TONS;

                    cmd.Parameters.Add(
                        "LD2_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD2_TONS;

                    cmd.Parameters.Add(
                        "LD3_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD3_TONS;

                    cmd.Parameters.Add(
                        "MRDTP_TONS",
                        OracleDbType.Decimal).Value =
                        model.MRDTP_TONS;

                    cmd.Parameters.Add(
                        "NOOFTP",
                        OracleDbType.Decimal).Value =
                        model.NOOFTP;

                    cmd.Parameters.Add(
                        "DATE_TIME_PROD_F",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME_PROD_F;

                    cmd.ExecuteNonQuery();
                }
            }
            else
            {
                string insertQry = @"

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
                        TO_DATE(:DATE_TIME,
                        'DD-MM-YYYY HH24:MI:SS'),

                        :LD1_TONS,
                        :LD2_TONS,
                        :LD3_TONS,

                        :MRDTP_TONS,
                        :NOOFTP,

                        :LD1_TONS_ACTUAL,
                        :LD2_TONS_ACTUAL,
                        :LD3_TONS_ACTUAL,

                        :MRDTP_TONS_ACTUAL,

                        'A-F'
                    )";

                using (OracleCommand cmd =
                    new OracleCommand(insertQry, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    cmd.Parameters.Add(
                        "LD1_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD1_TONS;

                    cmd.Parameters.Add(
                        "LD2_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD2_TONS;

                    cmd.Parameters.Add(
                        "LD3_TONS",
                        OracleDbType.Decimal).Value =
                        model.LD3_TONS;

                    cmd.Parameters.Add(
                        "MRDTP_TONS",
                        OracleDbType.Decimal).Value =
                        model.MRDTP_TONS;

                    cmd.Parameters.Add(
                        "NOOFTP",
                        OracleDbType.Decimal).Value =
                        model.NOOFTP;

                    cmd.Parameters.Add(
                        "LD1_TONS_ACTUAL",
                        OracleDbType.Decimal).Value =
                        model.LD1_TONS_ACTUAL;

                    cmd.Parameters.Add(
                        "LD2_TONS_ACTUAL",
                        OracleDbType.Decimal).Value =
                        model.LD2_TONS_ACTUAL;

                    cmd.Parameters.Add(
                        "LD3_TONS_ACTUAL",
                        OracleDbType.Decimal).Value =
                        model.LD3_TONS_ACTUAL;

                    cmd.Parameters.Add(
                        "MRDTP_TONS_ACTUAL",
                        OracleDbType.Decimal).Value =
                        model.MRDTP_TONS_ACTUAL;

                    cmd.ExecuteNonQuery();
                }
            }

            #endregion

            #region G PLANT

            int VCountG = 0;

            string countQryG = @"

                SELECT COUNT(*)

                FROM DEMO.T_LADLE

                WHERE DATE_TIME =
                      TO_DATE(:DATE_TIME_PROD_F,
                      'DD-MM-YYYY HH24:MI:SS')

                AND PLANT='G'";

            using (OracleCommand cmd =
                new OracleCommand(countQryG, con))
            {
                cmd.Transaction = trans;

                cmd.Parameters.Add(
                    "DATE_TIME_PROD_F",
                    OracleDbType.Varchar2).Value =
                    model.DATE_TIME_PROD_F;

                VCountG = Convert.ToInt32(
                    cmd.ExecuteScalar());
            }

            if (VCountG > 0)
            {
                string updateQryG = @"

                    UPDATE DEMO.T_LADLE

                    SET
                        DATE_TIME =
                        TO_DATE(:DATE_TIME,
                        'DD-MM-YYYY HH24:MI:SS'),

                        LD1_TONS = NULL,
                        LD2_TONS = NULL,
                        LD3_TONS = NULL,

                        MRDTP_TONS = NULL,

                        NOOFTP = :NOOFTP_G

                    WHERE DATE_TIME =
                          TO_DATE(:DATE_TIME_PROD_F,
                          'DD-MM-YYYY HH24:MI:SS')

                    AND PLANT='G'";

                using (OracleCommand cmd =
                    new OracleCommand(updateQryG, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    cmd.Parameters.Add(
                        "NOOFTP_G",
                        OracleDbType.Decimal).Value =
                        model.NOOFTP_G;

                    cmd.Parameters.Add(
                        "DATE_TIME_PROD_F",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME_PROD_F;

                    cmd.ExecuteNonQuery();
                }
            }
            else
            {
                string insertQryG = @"

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
                        TO_DATE(:DATE_TIME,
                        'DD-MM-YYYY HH24:MI:SS'),

                        NULL,
                        NULL,
                        NULL,

                        NULL,

                        :NOOFTP_G,

                        :LD1_TONS_ACTUAL_G,
                        :LD2_TONS_ACTUAL_G,
                        :LD3_TONS_ACTUAL_G,

                        :MRDTP_TONS_ACTUAL_G,

                        'G'
                    )";

                using (OracleCommand cmd =
                    new OracleCommand(insertQryG, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    cmd.Parameters.Add(
                        "NOOFTP_G",
                        OracleDbType.Decimal).Value =
                        model.NOOFTP_G;

                    cmd.Parameters.Add(
                        "LD1_TONS_ACTUAL_G",
                        OracleDbType.Decimal).Value =
                        model.LD1_TONS_ACTUAL_G;

                    cmd.Parameters.Add(
                        "LD2_TONS_ACTUAL_G",
                        OracleDbType.Decimal).Value =
                        model.LD2_TONS_ACTUAL_G;

                    cmd.Parameters.Add(
                        "LD3_TONS_ACTUAL_G",
                        OracleDbType.Decimal).Value =
                        model.LD3_TONS_ACTUAL_G;

                    cmd.Parameters.Add(
                        "MRDTP_TONS_ACTUAL_G",
                        OracleDbType.Decimal).Value =
                        model.MRDTP_TONS_ACTUAL_G;

                    cmd.ExecuteNonQuery();
                }
            }

            #endregion

            #region GET TP OT

            try
            {
                string qry = @"

                    SELECT NOOFTP, NOOFOT

                    FROM DEMO.T_LADLE

                    WHERE DATE_TIME =
                          TO_DATE(:DATE_TIME,
                          'DD-MM-YYYY HH24:MI:SS')

                    AND PLANT='A-F'";

                using (OracleCommand cmd =
                    new OracleCommand(qry, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    using (OracleDataReader dr =
                        cmd.ExecuteReader())
                    {
                        if (dr.Read())
                        {
                            vTotalTP =
                                dr["NOOFTP"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(
                                    dr["NOOFTP"]);

                            vTotalOT =
                                dr["NOOFOT"] == DBNull.Value
                                ? 0
                                : Convert.ToDecimal(
                                    dr["NOOFOT"]);
                        }
                    }
                }
            }
            catch
            {
            }

            #endregion

            #region TOTAL TP PROD

            try
            {
                string qry = @"

                    SELECT SUM(NET_WT)

                    FROM DEMO.T_LADLE_DETAILS

                    WHERE TIMESTAMP =
                          TO_DATE(:DATE_TIME,
                          'DD-MM-YYYY HH24:MI:SS')

                    AND TRP_NO < 51";

                using (OracleCommand cmd =
                    new OracleCommand(qry, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    object result =
                        cmd.ExecuteScalar();

                    if (result != DBNull.Value)
                    {
                        vTotProdTP =
                            Convert.ToDecimal(result);
                    }
                }
            }
            catch
            {
            }

            #endregion

            #region HM TP

            try
            {
                if (vTotalTP > 0)
                {
                    vHMT_TP =
                        Math.Round(
                            (decimal)(vTotProdTP /
                            vTotalTP), 2);
                }
            }
            catch
            {
            }

            #endregion

            #region TOTAL OT PROD

            try
            {
                string qry = @"

                    SELECT SUM(NET_WT)

                    FROM DEMO.T_LADLE_DETAILS

                    WHERE TIMESTAMP =
                          TO_DATE(:DATE_TIME,
                          'DD-MM-YYYY HH24:MI:SS')

                    AND TRP_NO > 50";

                using (OracleCommand cmd =
                    new OracleCommand(qry, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add(
                        "DATE_TIME",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME;

                    object result =
                        cmd.ExecuteScalar();

                    if (result != DBNull.Value)
                    {
                        vTotProdOT =
                            Convert.ToDecimal(result);
                    }
                }
            }
            catch
            {
            }

            #endregion

            #region HM OT

            try
            {
                if (vTotalOT > 0)
                {
                    vHMT_OT =
                        Math.Round(
                            (decimal)(vTotProdOT /
                            vTotalOT), 2);
                }
            }
            catch
            {
            }

            #endregion

            #region UPDATE HM

            string updateHM = @"

                UPDATE DEMO.T_LADLE

                SET
                    HM_TONS_PER_OT = :HM_TONS_PER_OT,
                    HM_TONS_PER_TP = :HM_TONS_PER_TP

                WHERE DATE_TIME =
                      TO_DATE(:DATE_TIME,
                      'DD-MM-YYYY HH24:MI:SS')

                AND PLANT='A-F'";

            using (OracleCommand cmd =
                new OracleCommand(updateHM, con))
            {
                cmd.Transaction = trans;

                cmd.Parameters.Add(
                    "HM_TONS_PER_OT",
                    OracleDbType.Decimal).Value =
                    (object)vHMT_OT ?? DBNull.Value;

                cmd.Parameters.Add(
                    "HM_TONS_PER_TP",
                    OracleDbType.Decimal).Value =
                    (object)vHMT_TP ?? DBNull.Value;

                cmd.Parameters.Add(
                    "DATE_TIME",
                    OracleDbType.Varchar2).Value =
                    model.DATE_TIME;

                cmd.ExecuteNonQuery();
            }

            #endregion

            #region PROCEDURE CALL

            try
            {
                using (OracleCommand cmd =
                    new OracleCommand(
                        "DEMO.PROC_LADLE_TODATE", con))
                {
                    cmd.Transaction = trans;

                    cmd.CommandType =
                        CommandType.StoredProcedure;

                    cmd.Parameters.Add(
                        "P_DATE",
                        OracleDbType.Varchar2).Value =
                        model.DATE_TIME_PROD_C;

                    cmd.ExecuteNonQuery();
                }
            }
            catch
            {
            }

            #endregion

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
