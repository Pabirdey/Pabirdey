CREATE OR REPLACE VIEW VW_FURNACE_MATERIAL AS
SELECT 
    b.TAG_ID,
    b.FUR_NAME,
    b.WEB_SL_NO,
    b.WEB_COLUMN,
    a.Timestamp,
    NVL(a.VALUE,0) AS VALUE,
    
    /* Value Kgs */
    CASE 
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' 
            THEN NVL(a.VALUE,0) * 1000
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0)
        ELSE NVL(a.VALUE,0)
    END AS VAL_KGS,

    /* Value Tons */
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
  AND b.WEB_COLUMN IS NOT NULL;