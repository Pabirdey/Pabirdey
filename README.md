select Timestamp,AVG(ROUND(SUM(Nvl(NC_RATE,0)*PRODUCTION)/SUM(PRODUCTION),1)*SUM(PRODUCTION)/1000) NUT_COKE_GEN_BF1 
FROM  kpo.t_kpo_bf_production_daily WHERE FUR_NO='KPO_BF1'  
AND   Timestamp>=sysdate-50
Group by Timestamp
Order by Timestamp;
