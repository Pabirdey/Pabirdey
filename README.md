sqlstr = "SELECT Count(t_ladle_details.FILL_STATUS) TOTAL_RUNNING_HR FROM demo.t_ladle_details "
sqlstr = sqlstr + " WHERE (LADLE_FLEND_TIME>='" & vfr_date & "' And LADLE_FLEND_TIME<='" & vdate & "') AND (TRP_NO=" & vTrp_No & ") AND (RET_FLAG='N')"
rs.Open sqlstr, con, adOpenStatic, adLockOptimistic
       If rs!TOTAL_RUNNING_HR = 0 Or IsNull(rs!TOTAL_RUNNING_HR) = True Then
            Sheets("Report").Cells(i, 3) = "RELINE"
        Else
            Sheets("Report").Cells(i, 3) = rs!TOTAL_RUNNING_HR
       End If
   rs.Close
    If Sheets("Report").Cells(i, 3) = "RELINE" Then
        Range("E" & i & ":T" & i) = ""
        ''''''''''''''
    Else
       If Sheets("Report").Cells(i, 3) = "RELINE" Then
        Sheets("Report").Cells(i, 5) = ""
        Else
        Sheets("Report").Cells(i, 5) = (Sheets("Report").Cells(i, 3) / Sheets("Report").Cells(i, 4)) * 100
       End If
