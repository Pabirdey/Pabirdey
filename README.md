SELECT 
    grp,
    SUM(LD1_TONS_ACTUAL) AS LD1_TONS_ACT
FROM (
    SELECT 
        LD1_TONS_ACTUAL,
        CASE 
            WHEN PLANT = 'A-F' THEN 'A-F'
            WHEN PLANT IN ('A-F','G') THEN 'A-G'
            WHEN PLANT IN ('A-F','G','H') THEN 'A-H'
            WHEN PLANT IN ('A-F','G','H','I') THEN 'A-I'
        END grp
    FROM DEMO.T_LADLE
    WHERE DATE_TIME >= TO_DATE('01-APR-2026','DD-MON-YYYY')
      AND DATE_TIME <  TO_DATE('14-APR-2026','DD-MON-YYYY')
)
GROUP BY grp
ORDER BY grp;