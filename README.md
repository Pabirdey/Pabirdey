SELECT 
    WK_TS,
    TO_NUMBER(SUBSTR(WK_TS, 9, 2)) AS WK_NO,
    AVG(
        ROUND(NC_RATE_PROD / NULLIF(TOTAL_PROD,0), 1)
        * TOTAL_PROD / 1000
    ) AS NUT_COKE_GEN_BF1
FROM (
    SELECT 
        WEEK(Timestamp) AS WK_TS,
        SUM(NVL(NC_RATE,0) * PRODUCTION) AS NC_RATE_PROD,
        SUM(PRODUCTION) AS TOTAL_PROD
    FROM kpo.t_kpo_bf_production_daily
    WHERE FUR_NO = 'KPO_BF1'
      AND Timestamp >= SYSDATE - 100
      AND TO_NUMBER(SUBSTR(WEEK(Timestamp),9,2)) >= 1
    GROUP BY WEEK(Timestamp)
) t
GROUP BY WK_TS
ORDER BY WK_TS;