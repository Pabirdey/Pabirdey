CREATE OR REPLACE PROCEDURE Proc_Get_BF_Raw_Material
(
    p_furnace IN VARCHAR2,
    p_date    IN DATE,
    p_cursor  OUT SYS_REFCURSOR
)
AS
    v_count NUMBER;
BEGIN

    EXECUTE IMMEDIATE 'ALTER SESSION SET NLS_DATE_FORMAT=''DD-MON-YYYY HH24:MI:SS''';

    SELECT COUNT(*)
    INTO v_count
    FROM TEST.T_FURNACES_PROC_HM_PROD a,
         IMTG.T_ATOF_BIN_DETAILS b
    WHERE b.TAG_ID = a.TAG_ID
      AND b.REQUIRED = 'Y'
      AND b.WEB_COLUMN IS NOT NULL
      AND a.TIMESTAMP = p_date
      AND b.FUR_NAME = p_furnace;

    IF v_count > 0 THEN

        OPEN p_cursor FOR

        SELECT
            b.TAG_ID,
            b.WEB_COLUMN AS MATERIAL_NAME,

            -- VALUE_TON
            CASE
                WHEN b.FUR_NAME = 'C'
                    THEN NVL(a.VALUE,0)
                ELSE
                    NVL(a.VALUE,0) / 1000
            END AS VALUE_TON,

            -- VALUE_KG
            CASE
                WHEN b.FUR_NAME = 'C'
                    THEN NVL(a.VALUE,0) * 1000
                ELSE
                    NVL(a.VALUE,0)
            END AS VALUE_KG

        FROM IMTG.T_ATOF_BIN_DETAILS b,
             TEST.T_FURNACES_PROC_HM_PROD a

        WHERE b.TAG_ID = a.TAG_ID(+)
          AND a.TIMESTAMP(+) = p_date
          AND b.REQUIRED = 'Y'
          AND b.WEB_COLUMN IS NOT NULL
          AND b.FUR_NAME = p_furnace

        ORDER BY b.WEB_SL_NO;

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
        DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
/
