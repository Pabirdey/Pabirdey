 Begin
        For k in (
                        Select SAMPLE_DATE,PRODUCT,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSBSL',QUANTITY)))QTY_TSM_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSBSL',AL2O3)))AL2O3_TSM_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSBSL',K2O)))K2O_TSM_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSBSL',Fe)))FE_TSM_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSBSL',Phos)))PHOS_TSM_SO,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSBSL',QUANTITY)))QTY_TSM_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSBSL',AL2O3)))AL2O3_TSM_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSBSL',K2O)))K2O_TSM_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSBSL',Fe)))FE_TSM_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSBSL',Phos)))PHOS_TSM_BF,
                        AVG(Decode(PRODUCT,'SO',Decode(UPPER(DESTINATION),'KPO',QUANTITY)))QTY_KPO_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(UPPER(DESTINATION),'KPO',AL2O3)))AL2O3_KPO_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(UPPER(DESTINATION),'KPO',K2O)))K2O_KPO_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(UPPER(DESTINATION),'KPO',Fe)))FE_KPO_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(UPPER(DESTINATION),'KPO',Phos)))PHOS_KPO_SO,
                        AVG(Decode(PRODUCT,'BF',Decode(UPPER(DESTINATION),'KPO',QUANTITY)))QTY_KPO_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(UPPER(DESTINATION),'KPO',AL2O3)))AL2O3_KPO_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(UPPER(DESTINATION),'KPO',K2O)))K2O_KPO_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(UPPER(DESTINATION),'KPO',Fe)))FE_KPO_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(UPPER(DESTINATION),'KPO',Phos)))PHOS_KPO_BF,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSLPLJ',QUANTITY)))QTY_TSSIJ_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSLPLJ',AL2O3)))AL2O3_TSSIJ_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSLPLJ',K2O)))K2O_TSSIJ_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSLPLJ',Fe)))FE_TSSIJ_SO,
                        AVG(Decode(PRODUCT,'SO',Decode(DESTINATION,'TSLPLJ',Phos)))PHOS_TSSIJ_SO,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSLPLJ',QUANTITY)))QTY_TSSIJ_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSLPLJ',AL2O3)))AL2O3_TSSIJ_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSLPLJ',K2O)))K2O_TSSIJ_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSLPLJ',Fe)))FE_TSSIJ_BF,
                        AVG(Decode(PRODUCT,'BF',Decode(DESTINATION,'TSLPLJ',Phos)))PHOS_TSSIJ_BF
                        From T_KHONDBOND_ORE 
                        Where SAMPLE_DATE>=v_STDATE
                        Group by SAMPLE_DATE,PRODUCT
                        Order by SAMPLE_DATE)
        Loop
            Begin
                UPDATE imtg.T_RM_MIS_DAILY SET
                    DESPATCH_IRON_ORE=Decode(k.PRODUCT,'SO',k.QTY_TSM_SO,
                    DESPATCH_ALUMINA=Decode(k.PRODUCT,'SO',k.AL2O3_TSM_SO,Decode(k.PRODUCT,'BF',k.AL2O3_TSM_BF)),
                    ALKALI_K2O=Decode(k.PRODUCT,'SO',k.K2O_TSM_SO,Decode(k.PRODUCT,'BF',k.K2O_TSM_BF)),
                    FE=Decode(k.PRODUCT,'SO',k.FE_TSM_SO,Decode(k.PRODUCT,'BF',k.FE_TSM_BF)),
                    PHOS=Decode(k.PRODUCT,'SO',k.PHOS_TSM_SO,Decode(k.PRODUCT,'BF',k.PHOS_TSM_BF))
                    Where Timestamp=k.SAMPLE_DATE AND PLANT='TSM' AND PRODUCT='BF';                  
                                                                       
                
            Exception
            When Others Then 
            Dbms_output.put_line(SQLERRM);  
            End;
        End Loop;
        Commit;
   Commit;
   Exception
   When Others Then 
   Dbms_output.put_line(SQLERRM);  
   End;
   

END PROC_KHONDBOND_MIS_DAILY;
END PKG_RM_MIS_DAILY;
