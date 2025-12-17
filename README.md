SELECT 
    WEEK_TS,
    TO_NUMBER(SUBSTR(WEEK_TS, 9, 2)) AS WK_NO,
    AVG(RATE_PER_DAY) * AVG(PROD_TON) AS NUT_COKE_GEN_BF1
FROM (
    SELECT 
        WEEK(Timestamp) AS WEEK_TS,
        ROUND(
            SUM(NVL(NC_RATE,0) * PRODUCTION) 
            / NULLIF(SUM(PRODUCTION),0),
            1
        ) AS RATE_PER_DAY,
        SUM(PRODUCTION)/1000 AS PROD_TON
    FROM kpo.t_kpo_bf_production_daily
    WHERE FUR_NO = 'KPO_BF1'
      AND Timestamp >= SYSDATE - 100
    GROUP BY WEEK(Timestamp)
)
WHERE TO_NUMBER(SUBSTR(WEEK_TS,9,2)) >= 1
GROUP BY WEEK_TS
ORDER BY WEEK_TS;