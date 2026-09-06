If CDate(vttimestamp) >= CDate(vfr_date) Then
                Sheets("Report").Cells(i, 7) = CDate(vtrvdate) - CDate(vttimestamp) - 1
          Else
                Sheets("Report").Cells(i, 7) = ""
                If vttimestamp <> "" Then
                    Sheets("Report").Cells(i, 7) = 0
                End If
          End If
