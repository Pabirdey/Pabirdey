 string runningHrDisplay;
                        decimal maturityPerc=0;
                        if (totalRunningHr == 0)
                        {
                            runningHrDisplay = "RELINE";
                            model.TLC_MATURITY_PERC = null;
                            model.TLC_MAX_THERMAL_IMAGE = MaxThermalTimestamp;
                            model.TLC_THERMAL_VALUE = ThermalValue;
                            model.TLC_THERMAL_IMAGE_CONDITION = ThermalImage;
                            model.TLC_PLAN_SCAN_FREQUENCY = PlanScan;
                            model.TLC_HM_THROUGHPUT = HM_Through;
                            model.TLC_FILL_QTY_PER_TRIP = Fill_qty_Trip;
                            model.TLC_FUR_CIRCUIT = FurCircuit;
                            model.TLC_TARE_WT = TareWt;
                            model.TLC_LAST_REPAIR = MaxGunningTimestamp;
                            model.TLC_IR_SCAN = IR_SCAN_VALUE;

                        }
                        else
                        {
                            runningHrDisplay =totalRunningHr.ToString();
                              maturityPerc = (((decimal)totalRunningHr / vMaturity_Life) * 100);                            
                        }
