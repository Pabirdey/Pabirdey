
        [HttpPost]
        public JsonResult SaveLadleData(List<BFViewModel> modelList)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();                    
                    string checkQuery = @"SELECT COUNT(*) FROM DEMO.T_LADLE  WHERE DATE_TIME = :P_DATE  AND PLANT = 'G'";
                    int vCount = 0;

                    using (OracleCommand cmd = new OracleCommand(checkQuery, con))
                    {
                        cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE); 

                        vCount = Convert.ToInt32(cmd.ExecuteScalar());
                    }

                    if (vCount > 0)
                    {
                        
                        string updateQuery = @"UPDATE DEMO.T_LADLE
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
                            //cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Int32).Value = model.NOOFTP_G;
                            cmd.Parameters.Add(":P_OLD_DATE", OracleDbType.Date).Value = model.DATE_TIME_PROD_F;
                            cmd.ExecuteNonQuery();
                        }
                    }
                    else
                    {
                        
                        string insertQuery = @"INSERT INTO DEMO.T_LADLE
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
                            cmd.Parameters.Add(":P_DATE", OracleDbType.Date).Value = Convert.ToDateTime(model.PROD_DATE);
                            //cmd.Parameters.Add(":P_NOOFTP", OracleDbType.Int32).Value = model.NOOFTP_G;
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
          public class BFViewModel
    {

        public string FURNACE { get; set; }
        public DateTime PROD_DATE { get; set; }
        public decimal ACTUAL { get; set; }
        public decimal REPORTED { get; set; }
        public decimal BALANCE { get; set; }
        public decimal? ActualC { get; set; }
        public decimal? ReportedC { get; set; }
        public decimal? BalanceC { get; set; }

        public decimal? ACTUAL_C_TD { get; set; }
        public decimal? REPORTED_C_TD { get; set; }

        public decimal? ActualD { get; set; }
        public decimal? ReportedD { get; set; }
        public decimal? BalanceD { get; set; }

        public decimal? ACTUAL_D_TD { get; set; }
        public decimal? REPORTED_D_TD { get; set; }

        public decimal? ActualE { get; set; }
        public decimal? ReportedE { get; set; }
        public decimal? BalanceE { get; set; }

        public decimal? ACTUAL_E_TD { get; set; }
        public decimal? REPORTED_E_TD { get; set; }

        public decimal? ActualF { get; set; }
        public decimal? ReportedF { get; set; }
        public decimal? BalanceF { get; set; }

        public decimal? ACTUAL_F_TD { get; set; }
        public decimal? REPORTED_F_TD { get; set; }

        public decimal? DisplayActual { get; set; }
        public decimal? DisplayReported { get; set; }
        public decimal? DisplayActual_TD { get; set; }
        public decimal? DisplayReported_TD { get; set; }
        public decimal? DisplayBalance { get; set; }

        public decimal? LD1Tons { get; set; }
        public decimal? LD2Tons { get; set; }
        public decimal? LD3Tons { get; set; }
        public decimal? MRDTPTons { get; set; }

        public decimal ACT_LD1_TONS { get; set; }
        public decimal ACT_LD2_TONS { get; set; }
        public decimal ACT_LD3_TONS { get; set; }
        public decimal ACT_MRD_TP_TONS { get; set; }
        public decimal CTOG_LD1_TONS { get; set; }
        public decimal CTOG_LD2_TONS { get; set; }
        public decimal CTOG_LD3_TONS { get; set; }

        public decimal CTOG_MRDTP_TONS { get; set;}
        public decimal CTOH_LD1_TONS { get; set; }
        public decimal CTOH_LD2_TONS { get; set; }
        public decimal CTOH_LD3_TONS { get; set; }
        public decimal CTOH_MRDTP_TONS { get; set;}
        public decimal CTOI_LD1_TONS { get; set;}
        public decimal CTOI_LD2_TONS { get; set;}
        public decimal CTOI_LD3_TONS { get; set; }
        public decimal CTOI_MRDTP_TONS { get; set;}
        public decimal LD1_TONS_G { get; set; }
        public decimal LD2_TONS_G { get; set; }
        public decimal LD3_TONS_G { get; set; }
        public decimal MRDTP_TONS_G { get; set; }
        public decimal NOOFTP_G { get; set; }
        public decimal LD1_TONS_ACTUAL_G { get; set; }
        public decimal LD2_TONS_ACTUAL_G { get; set; }
        public decimal LD3_TONS_ACTUAL_G { get; set; }
        public decimal MRDTP_TONS_ACTUAL_G { get; set; }
        public decimal LD1_TONS_ACTUAL_TD_G { get; set; }
        public decimal LD2_TONS_ACTUAL_TD_G { get; set; }
        public decimal LD3_TONS_ACTUAL_TD_G { get; set; }
        public decimal MRD_TONS_ACTUAL_TD_G { get; set; }
        public decimal NO_TP_TD_G { get; set; }
        public decimal LD1_TONS_H { get; set; }
        public decimal LD2_TONS_H { get; set; }
        public decimal LD3_TONS_H { get; set; }
        public decimal MRDTP_TONS_H { get; set; }
        public decimal NOOFTP_H { get; set; }
        public decimal LD1_TONS_ACTUAL_H { get; set; }
        public decimal LD2_TONS_ACTUAL_H { get; set; }
        public decimal LD3_TONS_ACTUAL_H { get; set; }
        public decimal LD1_TONS_ACTUAL_TD_H { get; set; }
        public decimal MRDTP_TONS_ACTUAL_H { get; set; }
        public decimal LD2_TONS_ACTUAL_TD_H { get; set; }
        public decimal LD3_TONS_ACTUAL_TD_H { get; set; }
        public decimal MRD_TONS_ACTUAL_TD_H { get; set; }
        public decimal NO_TP_TD_H { get; set; }
        public decimal LD1_TONS_I { get; set; }

        public decimal LD2_TONS_I { get; set; }
        public decimal LD3_TONS_I { get; set; }
        public decimal MRDTP_TONS_I { get; set; }
        public decimal NOOFTP_I { get; set; }
        public decimal LD1_TONS_ACTUAL_I { get; set; }
        public decimal LD2_TONS_ACTUAL_I { get; set; }
        public decimal LD3_TONS_ACTUAL_I { get; set; }
        public decimal MRDTP_TONS_ACTUAL_I { get; set; }
        public decimal LD1_TONS_ACTUAL_TD_I { get; set; }
        public decimal LD2_TONS_ACTUAL_TD_I { get; set; }
        public decimal LD3_TONS_ACTUAL_TD_I { get; set; }
        public decimal MRD_TONS_ACTUAL_TD_I { get; set; }
        public decimal NO_TP_TD_I { get; set; }
        public decimal LD1_TONS_A_F { get; set; }
        public decimal LD2_TONS_A_F { get; set; }
        public decimal LD3_TONS_A_F { get; set; }
        public decimal MRDTP_TONS_A_F { get; set; }
        public decimal NOOFTP_A_F { get; set; }
        public decimal LD1_TONS_ACTUAL_A_F { get; set; }
        public decimal LD2_TONS_ACTUAL_A_F { get; set; }
        public decimal LD3_TONS_ACTUAL_A_F { get; set; }
        public decimal MRDTP_TONS_ACTUAL_A_F { get; set; }
        public decimal LD1_TONS_ACTUAL_TD_A_F { get; set; }
        public decimal LD2_TONS_ACTUAL_TD_A_F { get; set; }
        public decimal LD3_TONS_ACTUAL_TD_A_F { get; set; }
        public decimal MRD_TONS_ACTUAL_TD_A_F { get; set; }        
        public decimal NO_TP_TD_A_F { get; set; }


        public string ACT_PLANT { get; set; }

        public int? NoOfTP { get; set; }
        public BFViewModel()
        {
            Furnaces = new List<GBFTOIBFPRODUCTION>();


        }

        public List<GBFTOIBFPRODUCTION> Furnaces { get; set; }

        public decimal DISPLAY_ACTUAL { get; set; }

        public decimal DISPLAY_REPORTED { get; set; }

        public decimal DISPLAY_BALANCE { get; set; }

        public decimal DISPLAY_ACTUAL_TD { get; set; }

        public decimal DISPLAY_REPORTED_TD { get; set; }
    }
        public class GBFTOIBFPRODUCTION
    {
        #region BASIC DETAILS

        public string FURNACE { get; set; }

        public DateTime TIMESTAMP { get; set; }

        #endregion


        #region DAILY PRODUCTION

        public decimal ACTUAL { get; set; }

        public decimal REPORTED { get; set; }

        public decimal BALANCE { get; set; }

        #endregion


        #region TOTAL TO DATE

        public decimal ACTUAL_TD { get; set; }

        public decimal REPORTED_TD { get; set; }

        #endregion


        #region LADLE TONS

        public decimal LD1_TONS { get; set; }

        public decimal LD2_TONS { get; set; }

        public decimal LD3_TONS { get; set; }

        public decimal MRDTP_TONS { get; set; }

        public decimal NOOFTP { get; set; }

        #endregion


        #region ACTUAL LADLE TONS

        public decimal LD1_TONS_ACTUAL { get; set; }

        public decimal LD2_TONS_ACTUAL { get; set; }

        public decimal LD3_TONS_ACTUAL { get; set; }

        public decimal MRDTP_TONS_ACTUAL { get; set; }

        #endregion


        #region DISPLAY TOTAL

        public decimal DISPLAY_ACTUAL { get; set; }

        public decimal DISPLAY_REPORTED { get; set; }

        public decimal DISPLAY_BALANCE { get; set; }

        public decimal DISPLAY_ACTUAL_TD { get; set; }

        public decimal DISPLAY_REPORTED_TD { get; set; }

        #endregion
    }


