create or replace Procedure PROC_TSM_DRI_ALERT AS------CREATED BY PABIR ON DATE:-14-JAN-2026 AS PER REQUEST SULATA MADAM.
vMAXDATE DATE;
vTimestamp DATE;
v_days Number;
vPlant Varchar2(10);
vSTDATE DATE;
vCount Number;
vTODATE DATE;
Begin
Execute Immediate 'Alter session set nls_date_format=''DD-MON-YYYY HH24:MI:SS'''; 
Select Max(DATE_TIME) into vMAXDATE From TSBSL.T_TSM_DRI_ALERT;
    If vMAXDATE IS NULL THEN
        vMAXDATE:='01-JAN-2026';
    END IF;
    Select Add_MONTHS(trunc(SYSDATE,'MON'),-1) into vSTDATE From Dual;
       
     Begin
         For k in (Select SL_NO,PLANT,SOURCE,COLUMN_NAME,TAG_DECRIPTION,SOURCE_TABLE,DESTINATION_TABLE,LCL,UCL From TSBSL.T_TSM_DRI_ALERT_MASTER  Order by SL_NO)  
         Loop
            Begin
                  Select COUNT(*) into vCount From TSBSL.T_TSM_DRI_ALERT where DATE_TIME=vMAXDATE And PLANT=k.PLANT ;
                   If vCount=0 Then 
                    Insert into TSBSL.T_TSM_DRI_ALERT(DATE_TIME,PLANT,COLUMN_NAME)            
                    Values(vMAXDATE,k.PLANT,k.COLUMN_NAME); 
                   End If;
                   vSql:='Select '||k.SOURCE||' From '||k.SOURCE_TABLE||' Where DATE_TIME>='||vSTDATE '||' AND DATE_TIME<='||||'vMAXDATE'' AND PLANT=k.PLANT AND SL_NO=k.SL_NO;                     
                     Execute immediate vSql into vValue;                                                  
                      IF vValue < k.LCL OR v_value > k.UCL THEN            
                        vSql :='UPDATE ' || k.DESTINATION_TABLE || 'SET TOTAL_COUNT =NVL(TOTAL_COUNT,0)+vValue';
                        EXECUTE IMMEDIATE v_sql USING v_value, k.PLANT, k.COLUMN_NAME,k.SL_NO;
                      Elsif vValue < k.LCL THEN   
                        vSql :='UPDATE ' || k.DESTINATION_TABLE || 'SET COUNT_BEYOND_LCL_MIN =NVL(COUNT_BEYOND_LCL_MIN,0)+vValue';
                        EXECUTE IMMEDIATE v_sql USING v_value, k.PLANT, k.COLUMN_NAME,k.SL_NO;
                      Elsif vValue > k.UCL THEN   
                        vSql :='UPDATE ' || k.DESTINATION_TABLE || 'SET COUNT_BEYOND_UCL_MAX =NVL(COUNT_BEYOND_UCL_MAX,0)+vValue';
                        EXECUTE IMMEDIATE v_sql USING v_value, k.PLANT, k.COLUMN_NAME,k.SL_NO;                      
                    END IF;
            Exception
            When Others Then 
            DBMS_OUTPUT.PUT_LINE(SQLERRM);
            End;
         END Loop;
         Commit;
                      
     Exception
     When Others Then 
     DBMS_OUTPUT.PUT_LINE(SQLERRM);
     End;
     
Exception
When Others Then
DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
