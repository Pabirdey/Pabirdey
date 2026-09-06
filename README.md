 if (totalRunningHr == 0)
                        {
                            runningHrDisplay = "RELINE";
                            return
                        }
                        else
                        {
                            runningHrDisplay =totalRunningHr.ToString();
                              maturityPerc = (((decimal)totalRunningHr / vMaturity_Life) * 100);                            
                        }
