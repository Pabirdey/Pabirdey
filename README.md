CREATE OR REPLACE PROCEDURE Proc_Get_BF_Raw_Material
(
    p_furnace IN VARCHAR2,
    p_date    IN DATE,
    p_cursor  OUT SYS_REFCURSOR
)
AS
    v_count NUMBER;
BEGIN
    -- 🔹 Check if data exists
    SELECT COUNT(*)
    INTO v_count
    FROM t_furnaces_proc_hm_prod a
    JOIN T_ATOF_BIN_DETAILS b ON b.TAG_ID = a.TAG_ID
    WHERE b.REQUIRED = 'Y'
      AND b.WEB_COLUMN IS NOT NULL
      AND a.TIMESTAMP = p_date
      AND b.FUR_NAME = p_furnace;

    -- 🔹 If data exists → FIRST query
    IF v_count > 0 THEN
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
        ORDER BY WEB_SL_NO;

    -- 🔹 If NO data → SECOND query
    ELSE
        OPEN p_cursor FOR
        SELECT WEB_COLUMN
        FROM imtg.T_ATOF_BIN_DETAILS
        WHERE REQUIRED = 'Y'
          AND WEB_COLUMN IS NOT NULL
          AND FUR_NAME = p_furnace
        ORDER BY WEB_SL_NO;
    END IF;

EXCEPTION
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20001, SQLERRM);
END;
/