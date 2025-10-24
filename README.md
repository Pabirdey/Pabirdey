Select b.Timestamp Date_Month,'TSK_PELLET' AS PLANT,ROUND((a.ACTUAL_QUANTITY))NET_PROD,
ROUND(b.NET_PRODUCTIVITY,2)NET_PRODUCTIVITY,NULL,
Round(c.FE,2)FE,Round(c.CAO/Nullif(c.SIO2,0),2)B2,
Round(c.AL2O3,3)AL2O3,Round(c.P,3)Phos,
Round(c.K2O,3)K2O,ROUND(d.AVG_CCS)CCS_CRMT,Round(c.PCT_TUM_6P3MM,1)TUMBLER_PLS_6P3_MM,
Round(c.PLS_TUM_MIN_0P5MM,3)TUMBLER_MIN_0P5_MM,ROUND(AVG(e.RDI),2)RDI,ROUND(AVG(f.RI),2)RI,
Round(AVG(g.SWELLING_INDEX),2)SWELLING_INDEX_CRMT,
AVG((nvl(h.ENG_CONS_DRYER_1,0)+nvl(i.ENG_CONS_DRYER_2,0))/
Decode(((Case When h.ENG_CONS_DRYER_1>0 Then 1 Else 0 END)+
(Case When i.ENG_CONS_DRYER_2>0 Then 1 Else 0 END)),0,null,
((Case When h.ENG_CONS_DRYER_1>0 Then 1 Else 0 END)+(Case When i.ENG_CONS_DRYER_2>0 Then 1 Else 0 END))))ENG_CONS,NULL,NULL,NULL
FROM KPO.T_KPO_COST_DATA a,KPO.T_KPO_PELLET_PROD_MONTHLY b,KPO.t_kpo_Pellet_quality_monthly c ,
KPO.T_KPO_PELLET_CCS_MONTHLY d,KPO.T_KPO_PELLET_RDI_DAILY e, KPO.T_KPO_PELLET_RI_DAILY f,
KPO.T_KPO_PELLET_SWELLING_INDEX_DAILY g,KPO.T_KPO_PELLET_DRYING_GRIND_PROCESS_DAILY h,
kpo.T_KPO_PELLET_DRYGRIND_STREAM2_DAILY i
Where c.SOURCE(+)='PRODUCT' AND c.PLANT(+)='KPO-Pellet Plant'
AND a.AREA(+)='100028600' AND a.COST_TYPE(+)='MC' AND a.COST_ELEMENT(+)='111105481'
AND  b.Timestamp=c.DATE_MONTH(+) AND b.Timestamp=d.DATE_MONTH(+)
AND b.Timestamp=Trunc(e.DATE_Time(+),'MON') AND b.Timestamp=Trunc(f.DATE_Time(+),'MON')AND 
b.Timestamp=Trunc(g.DATE_Time(+),'MON')AND b.Timestamp=Trunc(a.DATE_Time(+),'MON') AND 
trunc(b.Timestamp)=Trunc(h.Timestamp(+),'MON')AND trunc(b.Timestamp)=Trunc(i.Timestamp(+),'MON') AND 
Trunc(g.Date_Time,'MON')<Trunc(SYSDATE,'MOn')  AND 
Trunc(f.Date_Time,'MON')<Trunc(SYSDATE,'MOn')  AND
Trunc(e.Date_Time,'MON')<Trunc(SYSDATE,'MOn')  AND
Trunc(h.Timestamp,'MON')<Trunc(SYSDATE,'MOn')  AND
Trunc(i.Timestamp,'MON')<Trunc(SYSDATE,'MOn')  AND
b.Timestamp>=sysdate-200
Group by b.Timestamp,b.NET_PRODUCTIVITY,c.FE,c.CAO,c.SIO2,c.AL2O3,c.P,
c.K2O,d.AVG_CCS,c.PCT_TUM_6P3MM,c.PLS_TUM_MIN_0P5MM,a.ACTUAL_QUANTITY
Order by b.Timestamp
