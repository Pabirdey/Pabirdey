decimal? ThermalValue = null;

if (MaxThermalTimestamp.HasValue)
{
    DateTime vttimestamp = MaxThermalTimestamp.Value;

    if (vttimestamp >= vfr_date)
    {
        ThermalValue = (decimal)(vdate_Trunc - vttimestamp).TotalDays - 1;
    }
    else
    {
        ThermalValue = 0;
    }
}
