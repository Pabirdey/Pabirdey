Begin
  For k in (Select DATE_TIME,BM_CONS,FLUX_TRIM,Lime_Trim,Coke_Trim,SINTER_RET_FINES_ATOF,SINTER_RET_FINES_G,SINTER_RET_FINES_H,SINTER_RET_FINES_I From imtg.T_SP1_PRODUCTION Where Date_Time>=sysdate-500 Order by Date_Time)
  Loop
    Begin
        Update imtg.T_SINTER_MIS_DAILY SET
       BASE_MIX=k.BM_CONS/Decode((nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0)),0,null,(nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0))*100,        
        LIME_STONE=k.FLUX_TRIM/Decode((nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0)),0,null,(nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0))*100,        
        LIME=k.Lime_Trim/Decode((nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0)),0,null,nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0))*100,        
        COKE_BREEZE=k.Coke_Trim/Decode((nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0)),0,null,(nvl(k.FLUX_TRIM,0)+nvl(k.Lime_Trim,0)+nvl(k.Coke_Trim,0)+nvl(k.SINTER_RET_FINES_ATOF,0)+nvl(k.SINTER_RET_FINES_H,0)+nvl(k.SINTER_RET_FINES_G,0)+nvl(k.SINTER_RET_FINES_I,0))*100
        Where DATE_TIME=Timestamp AND PLANT='SP1';   
    Exception
    When Others Then  
    DBMS_OUTPUT.PUT_LINE(SQLERRM);
    End;
  End Loop;
  Exception
  When Others Then 
  DBMS_OUTPUT.PUT_LINE(SQLERRM);
  END;
