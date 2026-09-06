decimal? ThermalValue = null;

                        if (MaxThermalTimestamp.HasValue)
                        {
                            DateTime vttimestamp = MaxThermalTimestamp.Value;

                            if (vttimestamp >= vfr_date)
                            {
                                ThermalValue = (vdate_Trunc- vttimestamp);
                            }
                            else
                            {
                                ThermalValue = 0;
                            }
                        }
