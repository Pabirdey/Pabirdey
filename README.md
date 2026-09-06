sqlstr = "select max(timestamp) timestamp from t_thermal_imaging where timestamp>='" & vStDate & "' and timestamp<'" & vtrvdate & "'  and TLC_NO_THERMAL_IMAGING=" & vTrp_No & ""
