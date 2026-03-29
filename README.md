  For k in(SELECT TIMESTAMP,FURNACE,ACTUAL,REPORTED,BALANCE From Demo.T_BF_PRODUCTION_TRACKING Where TIMESTAMP=vDATE AND FURNACE in ('C','E','F') Order by FURNACE)
    Loop
        Begin
            Select COUNT(*) into vCount From demo.T_BF_PRODUCTION_BALANCE Where TIMESTAMP=k.TIMESTAMP AND FUR_NAME=K.FURNACE;
             IF vCount=0 Then      
                    Insert into demo.T_BF_PRODUCTION_BALANCE(TIMESTAMP,FUR_NAME,ACTUAL_ONDT,REPORTED_ONDT,BALANCE)
                    VALUES(K.TIMESTAMP,K.FURNACE,K.ACTUAL,K.REPORTED,K.BALANCE);                         
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
    
  FOR k in (SELECT TIMESTAMP,FURNACE,decode(sum(ACTUAL),0,Null,sum(ACTUAL))ACTUAL_TODT,decode(sum(REPORTED),0,Null,sum(REPORTED))REPORTED_TODT From Demo.T_BF_PRODUCTION_TRACKING Where TIMESTAMP>=V_TODT AND TIMESTAMP<=vDATE  AND FURNACE in ('C','E','F') GROUP BY FURNACE,TIMESTAMP Order by FURNACE)
  LOOP
        BEGIN
            UPDATE demo.T_BF_PRODUCTION_BALANCE SET
                            ACTUAL_TODT=k.ACTUAL_TODT,
                            REPORTED_TODT=k.REPORTED_TODT
            WHERE TIMESTAMP=k.TIMESTAMP AND FUR_NAME=K.FURNACE;                    
        EXCEPTION
        WHEN OTHERS THEN NULL;
        END;
  END LOOP;
COMMIT;
