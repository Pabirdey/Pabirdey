SELECT 
    TRUNC(a.timestamp,'MON') AS month_start,
    a.furnace,
    a.actual   AS act_ondt,
    a.reported AS report_ondt,
    a.balance,

    (
        SELECT SUM(b.actual)
        FROM demo.t_bf_production_balance b
        WHERE b.furnace = a.furnace
          AND b.timestamp >= TRUNC(a.timestamp,'MON')
          AND b.timestamp <= a.timestamp
    ) AS act_todt,

    (
        SELECT SUM(b.reported)
        FROM demo.t_bf_production_balance b
        WHERE b.furnace = a.furnace
          AND b.timestamp >= TRUNC(a.timestamp,'MON')
          AND b.timestamp <= a.timestamp
    ) AS report_todt

FROM demo.t_bf_production_balance a
WHERE a.timestamp = TO_DATE('11-APR-2026','DD-MON-YYYY')   -- ✅ FIX
ORDER BY a.furnace;
