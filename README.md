  int HM_Through = 0;
                        string HM_Through_query = @"
    SELECT ROUND(Sum(t_ladle_details.NET_WT)/1000) NET_WT
    FROM DEMO.T_LADLE_DETAILS
    WHERE LADLE_FLEND_TIME >= :finalDate
      AND LADLE_FLEND_TIME <= :vdate
      AND TRP_NO = :vTrp_No";

                        using (OracleCommand HM_Through_Cmd =
                               new OracleCommand(HM_Through_query, con))
                        {
                            HM_Through_Cmd.BindByName = true;

                            HM_Through_Cmd.Parameters.Add(":finalDate", OracleDbType.Date)
                                .Value = finalDate;

                            HM_Through_Cmd.Parameters.Add(":vdate", OracleDbType.Date)
                                .Value = vdate;

                            HM_Through_Cmd.Parameters.Add(":vTrp_No", OracleDbType.Int32)
                                .Value = vTrp_No;

                            object value = HM_Through_Cmd.ExecuteScalar();

                            if (value != null && value != DBNull.Value)
                            {
                                HM_Through = Convert.ToInt32(value);
                            }
                           
                        }
                        int? Fill_qty_Trip = 0;
                        Fill_qty_Trip = (int)(((decimal)HM_Through / totalRunningHr) * 1000);


                        model.TLC_ST_DATE = tlcStartDate;
                        model.TLC_END_DATE = tlcEndDate;
                        model.TLC_FINAL_DATE = finalDate; 
                        model.TLC_TOTAL_RUNNING_HR = totalRunningHr;
                        model.TLC_RUNNING_HR_DISPLAY = runningHrDisplay;
                        model.TLC_MATURITY_PERC= maturityPerc;
                        model.TLC_MAX_THERMAL_IMAGE=MaxThermalTimestamp;
                        model.TLC_THERMAL_VALUE= ThermalValue;
                        model.TLC_THERMAL_IMAGE_CONDITION= ThermalImage;
                        model.TLC_PLAN_SCAN_FREQUENCY=PlanScan;
                        model.TLC_HM_THROUGHPUT= HM_Through;
                        model.TLC_FILL_QTY_PER_TRIP = Fill_qty_Trip;
                        list.Add(model);
