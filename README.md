create or replace PROCEDURE PROC_TSMD_RAWMAT_ANALYSIS AS
vDate_Time  Date;
vCount      Number;
vCountRec   Number;
vID         Number;
vSample_date Date;
Begin
    Execute Immediate 'Alter session set nls_date_format=''DD-MON-YYYY HH24:MI:SS'''; 
    Select Max(TIMESTAMP)-7 into vDate_Time  From TMET.T_TSMD_RAW_MAT_ANALYSIS;
    If vDate_Time is Null Then        
        vDate_Time:='01-APR-2024';
    End If;   

    For i in ( 
            Select DISTINCT(a.RUN_ID) RUN_ID,b.MAT_NO,b.MAT_NAME,'BF1' AS PLANT ,a.* From BFL2.T_LAB_MANUAL_ENTRY_DATA@MBF1 a ,TMET.T_TSMD_RAW_MATERIAL_MASTER b
            Where a.MATERIAL_ID=b.L2_MATERIAL_ID AND a.TIMESTAMP>=vDate_Time
            UNION 
            Select DISTINCT(c.RUN_ID) RUN_ID,d.MAT_NO,d.MAT_NAME,'BF2' AS PLANT,c.* From TMLBF2.T_LAB_MANUAL_ENTRY_DATA@MBF2 c,
            TMET.T_TSMD_RAW_MATERIAL_MASTER d Where c.MATERIAL_ID=d.L2_MATERIAL_ID And c.TIMESTAMP>=vDate_Time
            )
    Loop
        Begin
            Select Count(*) into vCount from TMET.T_TSMD_RAW_MAT_ANALYSIS where RUN_ID=i.RUN_ID AND PLANT=i.PLANT AND MAT_NAME=i.MAT_NAME AND MAT_NO=i.MAT_NO;
            If vCount=0 Then                
                Insert into TMET.T_TSMD_RAW_MAT_ANALYSIS 
                (TIMESTAMP,PLANT,MAT_NAME,MAT_NO,FE_T,FE2O3,CAO,SIO2,S,MGO,MNO,MN,AL2O3,TIO2,CR2O3,C,P,MOISTURE,NA2O,K2O,B2,B3,LOI,TUMBLER_INDEX,ABRASION_INDEX,
                 CRI,ASH,MINUS_5MM,PLUS_10MM,RDI,RI,VM,UPDATE_MODE,RUN_ID)         
                 (Select i.TIMESTAMP,i.PLANT,i.MAT_NAME,i.MAT_NO,i.FE_T,i.FE2O3,i.CAO,i.SIO2,i.S,i.MGO,i.MNO,i.MN,i.AL2O3,i.TIO2,i.CR2O3,i.C,i.P,
                 i.MOISTURE,i.NA2O,i.K2O,i.B2,i.B3,i.LOI,i.TUMBLER_INDEX,i.ABRASION_INDEX,i.CRI,i.ASH,i.MINUS_5MM,i.PLUS_10MM,i.RDI,i.RI,i.VM,i.UPDATE_MODE,RUN_ID)                
            Else
                Update TMET.T_TSMD_RAW_MAT_ANALYSIS b set 
                FE_T=i.FE_T,
                FE2O3=i.FE2O3,
                CAO=i.CAO,
                SIO2=i.SIO2,
                S=i.S,
                MGO=i.MGO,
                MNO=i.MNO,
                MN=i.MN,
                AL2O3=i.AL2O3,
                TIO2=i.TIO2,
                CR2O3=i.CR2O3,
                C=i.C,
                P=i.P,
                MOISTURE=i.MOISTURE,
                NA2O=i.NA2O,
                K2O=i.K2O,
                B2=i.B2,
                B3=i.B3,
                LOI=i.LOI,
                TUMBLER_INDEX=i.TUMBLER_INDEX,
                ABRASION_INDEX=i.ABRASION_INDEX,
                CRI=i.CRI,
                ASH=i.ASH,
                MINUS_5MM=i.MINUS_5MM,
                PLUS_10MM=i.PLUS_10MM,
                RDI=i.RDI,
                RI=i.RI,
                VM=i.VM,
                UPDATE_MODE=i.UPDATE_MODE,
                RUN_ID=i.RUN_ID                
                Where b.TIMESTAMP=i.TIMESTAMP AND b.RUN_ID=i.RUN_ID AND b.MAT_NAME=i.MAT_NAME AND b.PLANT=i.PLANT AND b.MAT_NO=i.MAT_NO;          
            End If;
            Commit;
        Exception
        When Others Then
        DBMS_OUTPUT.PUT_LINE(SQLERRM);
        End;
    End Loop;
EXCEPTION
 When Others Then
 DBMS_OUTPUT.PUT_LINE(SQLERRM ||'-PROC_TSMD_RAWMAT_ANALYSIS');
End PROC_TSMD_RAWMAT_ANALYSIS;
