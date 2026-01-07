 Begin
            Update T_DRI_MIS_MONTHLY
            Set CAPACITY=(Select Case When CAPACITY=500 Then CAPACITY*to_number(to_char(last_day(Timestamp),'DD')) Else NUll END
            From TSBSL.T_TSM_DRI_MIS_DAILY Where PLANT in ('TSM_KILN1','TSM_KILN2','TSM_KILN3','TSM_KILN4','TSM_KILN5','TSM_KILN6','TSM_KILN7','TSM_KILN8','TSM_KILN9','TSM_KILN10'));
            Commit;            
        Exception
        When Others Then
        DBMS_OUTPUT.PUT_LINE(SQLERRM);
        End;
