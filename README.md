create or replace Procedure PROC_SINTER_MIS_MONTHLY AS
vMaxMonth Date;
vCount Number;
Begin
 Execute immediate 'Alter Session set nls_date_Format=''DD-MON-YYYY''';
 For k in (Select Distinct(PLANT) From imtg.T_SINTER_MIS_DAILY)
            Loop
                Begin
                    Select TRUNC(Max(Timestamp),'MON') into vMaxMonth From imtg.T_SINTER_MIS_MONTHLY Where PLANT=i.PLANT;
                    If Trunc(SYSDATE,'MON')=vMaxMonth Then
                    vMaxMonth:=ADD_MONTH(vMaxMonth-1);
                    Elsif vMaxMonth IS NULL Then
                    vMaxMonth:='01-APR-2024';                        
                    End If;
                    For i in (Select 
                            Trunc(Timestamp,'MON')Timestamp,
                            SUM(Case GROSS_PRODUCTION>0 Then GROSS_PRODUCTION Else NULL END)GROSS_PRODUCTION,
                            SUM(Case PSW_CONSUMPTION >0 Then PSW_CONSUMPTION Else NULL END)PSW_CONSUMPTION ,
                            AVG(Case LIME_PERC>0 Then LIME_PERC Else NULL END)LIME_PERC,
                            AVG(Case AVAILABILITY>0 Then AVAILABILITY Else NULL END)AVAILABILITY,
                            AVG(Case INTERNAL_RF>0 Then INTERNAL_RF Else NULL END)INTERNAL_RF,
                            AVG(Case MACHINE_SPEED   >0 Then MACHINE_SPEED   Else NULL END)MACHINE_SPEED   ,
                            AVG(Case WGT>0 Then WGT Else NULL END)WGT,
                            AVG(Case BTT>0 Then BTT Else NULL END)BTT,
                            AVG(Case SPM>0 Then SPM Else NULL END)SPM,
                            AVG(Case PRODUCT_SINTER_TEMP>0 Then PRODUCT_SINTER_TEMP Else NULL END)PRODUCT_SINTER_TEMP,
                            AVG(Case CARBON_RATE>0 Then CARBON_RATE Else NULL END)CARBON_RATE,
                            AVG(Case CAO>0 Then CAO Else NULL END)CAO,
                            AVG(Case SIO2>0 Then SIO2 Else NULL END)SIO2,
                            AVG(Case AL2O3>0 Then AL2O3 Else NULL END)AL2O3,
                            AVG(Case PHOS>0 Then PHOS Else NULL END)PHOS,
                            AVG(Case FEO>0 Then FEO Else NULL END)FEO,
                            AVG(Case RDI>0 Then RDI Else NULL END)RDI,
                            AVG(Case TI>0 Then TI Else NULL END)TI,
                            AVG(Case MEAN_SIZE>0 Then MEAN_SIZE Else NULL END)MEAN_SIZE,
                            AVG(Case DIRECT_DISPATCH >0 Then DIRECT_DISPATCH Else NULL END)DIRECT_DISPATCH ,
                            AVG(Case EXTERNAL_RF>0 Then EXTERNAL_RF Else NULL END)EXTERNAL_RF,
                            AVG(Case BIN_LEVEL_BF>0 Then BIN_LEVEL_BF Else NULL END)BIN_LEVEL_BF,
                            AVG(Case FUEL_RATE>0 Then FUEL_RATE Else NULL END)FUEL_RATE,
                            AVG(Case RI>0 Then RI Else NULL END)RI,
                            AVG(Case MGO>0 Then MGO Else NULL END)MGO,
                            AVG(Case ZN>0 Then ZN Else NULL END)ZN,
                            AVG(Case PSW_CONS_PER_NET_PROD>0 Then PSW_CONS_PER_NET_PROD Else NULL END)PSW_CONS_PER_NET_PROD,
                            SUM(Case NET_PRODUCTION  >0 Then NET_PRODUCTION  Else NULL END)NET_PRODUCTION  ,
                            AVG(Case CARBON_RATE_NET_PROD>0 Then CARBON_RATE_NET_PROD Else NULL END)CARBON_RATE_NET_PROD
                            From imtg.T_SINTER_MIS_DAILY Where Timestamp>=vMaxMonth AND Timestamp<Trunc(SYSDATE,'MON')
                            Group by Trunc(Timestamp,'MON'))  
                     Loop
                            Begin
                                Select COUNT(*) into vCOUNT From imtg.T_SINTER_MIS_MONTHLY Where PLANT=i.PLANT And Trunc(Timestamp,'MON')=j.Timestamp;
                                 If vCOUNT=0 Then
                                    Insert into imtg.T_SINTER_MIS_MONTHLY(Timestamp,Plant) Values(j.Timestamp,i.Plant);
                                 End If;
                                 Update imtg.T_SINTER_MIS_MONTHLY
                                 Set
                                GROSS_PRODUCTION=j.GROSS_PRODUCTION,
                                PSW_CONSUMPTION =j.PSW_CONSUMPTION ,
                                LIME_PERC       =j.LIME_PERC       ,
                                AVAILABILITY    =j.AVAILABILITY    ,
                                INTERNAL_RF     =j.INTERNAL_RF     ,
                                MACHINE_SPEED   =j.MACHINE_SPEED   ,
                                WGT             =j.WGT             ,
                                BTT             =j.BTT             ,
                                SPM             =j.SPM             ,
                                PRODUCT_SINTER_TEMP=j.PRODUCT_SINTER_TEMP,
                                CARBON_RATE     =j.CARBON_RATE     ,
                                CAO             =j.CAO             ,
                                SIO2            =j.SIO2            ,
                                AL2O3           =j.AL2O3           ,
                                PHOS            =j.PHOS            ,
                                FEO             =j.FEO             ,
                                RDI             =j.RDI             ,
                                TI              =j.TI              ,
                                MEAN_SIZE       =j.MEAN_SIZE       ,
                                DIRECT_DISPATCH =j.DIRECT_DISPATCH ,
                                EXTERNAL_RF     =j.EXTERNAL_RF     ,
                                BIN_LEVEL_BF    =j.BIN_LEVEL_BF    ,
                                FUEL_RATE       =j.FUEL_RATE       ,
                                RI              =j.RI              ,
                                MGO             =j.MGO             ,
                                ZN              =j.ZN              ,
                                PSW_CONS_PER_NET_PROD=j.PSW_CONS_PER_NET_PROD,
                                NET_PRODUCTION  =j.NET_PRODUCTION  ,
                                CARBON_RATE_NET_PROD =j.CARBON_RATE_NET_PROD 
                                Where Timestamp=j.Timestamp AND PLANT=j.PLANT;
                            Exception
                            When Others Then
                            DBMS_OUTPUT.PUT_LINE(SQLERRM);
                            END;                            
                     End Loop;
                    Commit;
                Exception
                When Others Then
                DBMS_OUTPUT.PUT_LINE(SQLERRM);
                END;
            End Loop;
Exception
When Others Then
DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
