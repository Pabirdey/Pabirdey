OPEN p_cursor FOR
SELECT
    b.WEB_COLUMN,
    NVL(a.VALUE,0) AS VALUE,
    CASE
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet'
            THEN NVL(a.VALUE,0) * 1000
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0)
        ELSE NVL(a.VALUE,0)
    END AS VAL_KGS,
    CASE
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet'
            THEN NVL(a.VALUE,0)
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0) / 1000
        ELSE NVL(a.VALUE,0) / 1000
    END AS VAL_TONS
FROM T_ATOF_BIN_DETAILS b
LEFT JOIN t_furnaces_proc_hm_prod a
       ON b.TAG_ID = a.TAG_ID
WHERE b.REQUIRED = 'Y'
  AND b.WEB_COLUMN IS NOT NULL
  AND a.TIMESTAMP = p_date
  AND b.FUR_NAME = p_furnace

UNION ALL

SELECT
    b.WEB_COLUMN,
    0 VALUE,
    0 VAL_KGS,
    0 VAL_TONS
FROM imtg.T_ATOF_BIN_DETAILS b
WHERE b.REQUIRED = 'Y'
  AND b.WEB_COLUMN IS NOT NULL
  AND b.FUR_NAME = p_furnace
  AND NOT EXISTS (
      SELECT 1
      FROM t_furnaces_proc_hm_prod a
      WHERE a.TIMESTAMP = p_date
  )
ORDER BY WEB_SL_NO;