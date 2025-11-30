SELECT 
    a.Timestamp,
    b.FUR_NAME,
    a.TAG_ID,
    b.WEB_SL_NO,
    b.WEB_COLUMN,

    /* VALUE IN KGS */
    CASE 
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' 
            THEN NVL(a.VALUE,0) * 1000
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0)
        ELSE NVL(a.VALUE,0)
    END AS VAL_KGS,

    /* VALUE IN TONS */
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
    AND a.Timestamp = TO_DATE('30-NOV-2025','DD-MON-YYYY')

WHERE b.REQUIRED = 'Y'
  AND b.WEB_COLUMN IS NOT NULL
ORDER BY a.TAG_ID, b.WEB_SL_NO;
