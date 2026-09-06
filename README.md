  int ? PlanScan=null;
                        string PlanScan_query = "SELECT Count(FILL_STATUS) TOTAL_RUNNING_HR FROM demo.t_ladle_details WHERE LADLE_FLEND_TIME>=vdate_Prev And LADLE_FLEND_TIME<=vdate AND TRP_NO=:vTrp_No AND RET_FLAG='N'";
                        using (OracleCommand PlanScanCmd =new OracleCommand(PlanScan_query, con))                        {
                            PlanScanCmd.Parameters.Add(":vdate_Prev", OracleDbType.Date).Value = vdate_Prev;
                            PlanScanCmd.Parameters.Add(":vdate", OracleDbType.Date).Value = vdate_Prev;
                            PlanScanCmd.Parameters.Add(":vTrpNo", OracleDbType.Int32).Value = vTrp_No;
                            object value = PlanScanCmd.ExecuteScalar();

                            if (value != null && value != DBNull.Value)
                            {
                                PlanScan = value.ToString();
                            }
                        }
