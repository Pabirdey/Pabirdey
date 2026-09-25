CREATE OR REPLACE PROCEDURE PROC_TSM_SP1_PROD_DAILY AS
vMaxdate Date;
v_Sql varchar2(32667);
Begin
EXECUTE IMMEDIATE 'ALTER SESSION SET NLS_DATE_FORMAT:=''DD-MON-YYYY HH24:MI:SS''';
SELECT MAX(TIMESTAMP)-7 INTO vMaxdate From TEST.T_TSBSL_SN_PROD_DAILY WHERE SOURCE='SP1';
IF vMaxdate IS NULL THEN
   vMaxdate:='01-APR-2026';
END IF;
    Begin
        for k in (Select SL_NO,SOURCE_TABLE,DESTINATION_TABLE,DEST_COLUMN,FREQUENCY From TEST.T_TSM_SP1_PROD_TAG_MASTER WHERE SOURCE='SP1' AND REQUIRED='Y' ORDER BY SL_NO)
                Loop
                    Begin
                        for t in (Select SL_NO,DATE_TIME,FREQUENCY,COLUMN_NAME,COLUMN_VALUE From TEST.T_TSM_SP1_PROD_RAW WHERE Date_Time>=vMaxdate AND COLUMN_NAME=k.DEST_COLUMN AND FREQUENCY=k.FREQUENCY AND SL_NO=k.SL_NO ORDER BY SL_NO)
                        Loop
                            Begin
                                Select COUNT(*) into vCount From TEST.T_TSBSL_SN_PROD_DAILY Where Source='SP1' AND Timestamp=t.Date_Time;
                                    If vCount=0 Then 
                                        
                                    End If;
                            Exception
                            When Others Then
                            DBMS_OUTPUT.PUT_LINE(SQLERRM);
                            End;
                        End Loop;                        
                    Exception
                    When Others Then 
                    DBMS_OUTPUT.PUT_LINE(SQLERRM);
                    End;                
                End Loop;
        
    Exception
    When Others Then
    DBMS_OUTPUT.PUT_LINE(SQLERRM);
    End;
Exception
WHEN OTHERS THEN 
DBMS_OUTPUT.PUT_LINE(SQLERRM);
End;
