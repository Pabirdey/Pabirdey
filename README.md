select WEEK(Timestamp) ,TO_NUMBER(SUBSTR(WEEK(Timestamp),9,2)) WK_NO,AVG((ROUND(SUM(Nvl(NC_RATE,0)*PRODUCTION)/SUM(PRODUCTION),1)))*AVG(SUM(PRODUCTION)/1000) NUT_COKE_GEN_BF1 
FROM  kpo.t_kpo_bf_production_daily WHERE FUR_NO='KPO_BF1'  
AND   Timestamp>=sysdate-100  AND to_number(substr(WEEK(Timestamp),9,2))>='1'  GROUP BY WEEK(Timestamp) ORDER BY  1
