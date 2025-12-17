SELECT 
    Timestamp,
    AVG(
        ROUND(
            (NC_RATE_PROD / NULLIF(TOTAL_PROD,0)), 
            1
        ) * TOTAL_PROD / 1000
    ) AS NUT_COKE_GEN_BF1
FROM (
    SELECT 
        Timestamp,
        SUM(NVL(NC_RATE,0) * PRODUCTION) AS NC_RATE_PROD,
        SUM(PRODUCTION) AS TOTAL_PROD
    FROM kpo.t_kpo_bf_production_daily
    WHERE FUR_NO = 'KPO_BF1'
      AND Timestamp >= SYSDATE - 50
    GROUP BY Timestamp
)
GROUP BY Timestamp
ORDER BY Timestamp;