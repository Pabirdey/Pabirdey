CREATE OR REPLACE PROCEDURE Proc_Get_BF_Raw_Material
(
    p_furnace IN VARCHAR2,
    p_date    IN DATE,
    p_cursor  OUT SYS_REFCURSOR
)
AS
    v_count NUMBER;
BEGIN

    ----------------------------------------------------------------
    -- Check if data exists (FIXED DATE COMPARISON)
    ----------------------------------------------------------------
    SELECT COUNT(*)
    INTO v_count
    FROM TEST.T_FURNACES_PROC_HM_PROD a
         JOIN IMTG.T_ATOF_BIN_DETAILS b
           ON b.TAG_ID = a.TAG_ID
    WHERE b.REQUIRED = 'Y'
      AND b.WEB_COLUMN IS NOT NULL
      AND b.FUR_NAME = p_furnace
      AND TRUNC(a.TIMESTAMP) = TRUNC(p_date);

    ----------------------------------------------------------------
    -- If data exists
    ----------------------------------------------------------------
    IF v_count > 0 THEN

        OPEN p_cursor FOR
            SELECT
                b.TAG_ID,
                b.WEB_COLUMN AS MATERIAL_NAME,

                CASE
                    WHEN b.FUR_NAME = 'F'
                         AND b.WEB_COLUMN = 'Pellet'
                    THEN ROUND(NVL(a.VALUE,0),2)

                    ELSE ROUND(NVL(a.VALUE,0) / 1000,2)
                END AS VALUE_TON,

                CASE
                    WHEN b.FUR_NAME = 'F'
                         AND b.WEB_COLUMN = 'Pellet'
                    THEN ROUND(NVL(a.VALUE,0) * 1000,2)

                    ELSE ROUND(NVL(a.VALUE,0),2)
                END AS VALUE_KG

            FROM IMTG.T_ATOF_BIN_DETAILS b
                 LEFT JOIN TEST.T_FURNACES_PROC_HM_PROD a
                   ON b.TAG_ID = a.TAG_ID
                  AND TRUNC(a.TIMESTAMP) = TRUNC(p_date)

            WHERE b.REQUIRED = 'Y'
              AND b.WEB_COLUMN IS NOT NULL
              AND b.FUR_NAME = p_furnace

            ORDER BY b.WEB_SL_NO;

    ----------------------------------------------------------------
    -- If NO data
    ----------------------------------------------------------------
    ELSE

        OPEN p_cursor FOR
            SELECT
                TAG_ID,
                WEB_COLUMN AS MATERIAL_NAME,
                0 AS VALUE_TON,
                0 AS VALUE_KG
            FROM IMTG.T_ATOF_BIN_DETAILS
            WHERE REQUIRED = 'Y'
              AND WEB_COLUMN IS NOT NULL
              AND FUR_NAME = p_furnace
            ORDER BY WEB_SL_NO;

    END IF;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
        RAISE;
END Proc_Get_BF_Raw_Material;
/
