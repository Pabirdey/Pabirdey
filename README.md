 string runningHrDisplay;
                        int maturityPerc;

                        if (totalRunningHr == 0)
                        {
                            runningHrDisplay = "RELINE";
                        }
                        else
                        {
                            runningHrDisplay =totalRunningHr.ToString();
                            maturityPerc = totalRunningHr / vMaturity_Life * 100;
                        }
