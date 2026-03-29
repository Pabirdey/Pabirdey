create or replace Procedure PROC_BF_PRODUCTION_BALANCE(vDATE DATE) AS-------CREATE BY PABIR ON DATE:-27-MARCH-2026.
vMaxDate Date;
vCount Number;
VDATE_TIME Date;
VFUR_NAME varchar2(20);
VACTUAL_ONDT number;
V_TODT Date;
Begin
Execute Immediate 'Alter session set NLS_DATE_FORMAT=''DD-MON_YYYY HH24:MI:SS''';
SELECT Max(Timestamp) into vMaxDate From Demo.T_BF_PRODUCTION_BALANCE;
SELECT TRUNC(SYSDATE,'MON') into V_TODT FROM DUAL;
If vMaxDate IS NULL Then
    vMaxDate:='01-JAN-2026';
END IF;
    For k in(SELECT TIMESTAMP,FURNACE,ACTUAL,REPORTED,BALANCE From Demo.T_BF_PRODUCTION_TRACKING Where TIMESTAMP=vDATE Order by FURNACE)
    Loop
        Begin
            Select COUNT(*) into vCount From demo.T_BF_PRODUCTION_BALANCE Where TIMESTAMP=k.TIMESTAMP AND FUR_NAME=K.FURNACE;
             IF vCount=0 Then      
                    Insert into demo.T_BF_PRODUCTION_BALANCE(TIMESTAMP,FUR_NAME,ACTUAL_ONDT,REPORTED_ONDT,BALANCE)
                    VALUES(K.TIMESTAMP,K.FURNACE,K.ACTUAL,K.REPORTED,K.BALANCE);            
             ELSif
             for i in (SELECT TIMESTAMP,FUR_NAME,SUM(NET_WT)NET_WT FROM DEMO.T_LADLE_DETAILS WHERE LADLE_FLEND_TIME>=Trunc(vDATE)+6/24 AND LADLE_FLEND_TIME<TRUNC(vDATE)+1+6/24    
                AND DESTINATION<>'R' GROUP BY FUR_NAME,TIMESTAMP ORDER BY FUR_NAME)
                LOOP
                      Insert into Demo.T_BF_PRODUCTION_BALANCE(TIMESTAMP,FUR_NAME,ACTUAL_ONDT)
                        VALUES(i.TIMESTAMP,i.FUR_NAME,i.NET_WT);  
                END LOOP;
             Else
                Update Demo.T_BF_PRODUCTION_BALANCE SET
                    ACTUAL_ONDT=k.ACTUAL,
                    REPORTED_ONDT=k.REPORTED,
                    BALANCE=k.BALANCE
                WHERE TIMESTAMP=K.TIMESTAMP AND FUR_NAME=K.FURNACE;                
            End If;   
        Exception
        When Others Then null;        
        End;        
    End Loop;
    COMMIT;   


Exception 
When Others Then null;
END;
