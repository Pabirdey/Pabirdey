Public Sub Plan_repair(i As Integer)
Dim vLife, vResult, vFur, vTrp, r, c

If i >= 7 And i <= 37 Then
    vTrp = ActiveSheet.Range("A" & i)
    vLife = ActiveSheet.Range("C" & i)
    vResult = ActiveSheet.Range("H" & i)
    vFur = ActiveSheet.Range("M" & i)
    ActiveSheet.Range("Q" & i) = ""
    If vTrp <> "" And vLife <> "" And vFur <> "" Then
        If vLife < 500 Then
            r = 138
        ElseIf vLife >= 500 And vLife < 1000 Then
            r = 139
        ElseIf vLife >= 1000 And vLife < 1300 Then
            r = 140
        ElseIf vLife >= 1300 And vLife < 1500 Then
            r = 141
        ElseIf vLife >= 1500 Then
            r = 142
        End If
     ''''''''''''''''''''''''''''''''''''''''''''''''''
        If vFur = "G" Or vFur = "H" Or vFur = "I" Then
            c = 27
        Else
            c = 26
        End If
      ''''''''''''''''''''''''''''''''''''''''''
        If vResult = "HIGH" Then
            c = c + 2
        End If
        
        ActiveSheet.Range("Q" & i) = ActiveSheet.Cells(r, c)
        
    End If
