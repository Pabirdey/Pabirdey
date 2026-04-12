SELECT Trunc(a.timestamp,'MON'),
    a.furnace,
    a.actual   AS act_ondt,
    a.reported AS report_ondt,
    a.balance,
    (
        SELECT
            SUM(b.actual)
        FROM
            demo.t_bf_production_balance b
        WHERE
            b.furnace = a.furnace
            AND b.timestamp >= trunc(
                a.timestamp, 'MON'
            )
            AND b.timestamp <= a.timestamp
    )          AS act_todt,
    (
        SELECT
            SUM(b.reported)
        FROM
            demo.t_bf_production_balance b
        WHERE
            b.furnace = a.furnace
            AND b.timestamp >= trunc(
                a.timestamp, 'MON'
            )
            AND b.timestamp <= a.timestamp
    )          AS report_todt
FROM
    demo.t_bf_production_balance a
WHERE
    a.timestamp ='11-APR-2026'
    
ORDER BY
    a.furnace
