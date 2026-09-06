sqlstr = "SELECT Count(t_ladle_details.FILL_STATUS) TOTAL_RUNNING_HR FROM demo.t_ladle_details "
sqlstr = sqlstr + " WHERE (LADLE_FLEND_TIME>='" & vfr_date & "' And LADLE_FLEND_TIME<='" & vdate & "') AND (TRP_NO=" & vTrp_No & ") AND (RET_FLAG='N')"
