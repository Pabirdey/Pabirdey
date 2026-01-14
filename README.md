CREATE OR REPLACE PROCEDURE PROC_TSM_DRI_ALERT
AS
    /* Variables */
    vMAXDATE   DATE;
    vSTDATE    DATE;
    vTODATE    DATE;
    vCount     NUMBER;
    vValue     NUMBER;
    vSql       CLOB;
BEGIN
    /* Get last processed date */
    SELECT MAX(DATE_TIME)
    INTO vMAXDATE
    FROM TSBSL.T_TSM_DRI_ALERT;

    IF vMAXDATE IS NULL THEN
        vMAXDATE := DATE '2026-01-01';
    END IF;

    /* Date range */
    vSTDATE := vMAXDATE;
    vTODATE := SYSDATE;

    /* Loop through master configuration */
    FOR k IN (
        SELECT SL_NO,
               PLANT,
               COLUMN_NAME,
               SOURCE_TABLE,
               DESTINATION_TABLE,
               LCL,
               UCL
        FROM TSBSL.T_TSM_DRI_ALERT_MASTER
        ORDER BY SL_NO
    )
    LOOP
        BEGIN
            /* Check record exists */
            SELECT COUNT(*)
            INTO vCount
            FROM TSBSL.T_TSM_DRI_ALERT
            WHERE DATE_TIME   = vMAXDATE
              AND PLANT       = k.PLANT
              AND COLUMN_NAME = k.COLUMN_NAME;

            IF vCount = 0 THEN
                INSERT INTO TSBSL.T_TSM_DRI_ALERT
                    (DATE_TIME, PLANT, COLUMN_NAME)
                VALUES
                    (vMAXDATE, k.PLANT, k.COLUMN_NAME);
            END IF;

            /* Dynamic select from source table */
            vSql :=
                'SELECT ' || k.COLUMN_NAME ||
                ' FROM ' || k.SOURCE_TABLE ||
                ' WHERE DATE_TIME BETWEEN :1 AND :2';

            EXECUTE IMMEDIATE vSql
                INTO vValue
                USING vSTDATE, vTODATE;

            /* Check limits */
            IF vValue < k.LCL OR vValue > k.UCL THEN

                vSql :=
                    'UPDATE ' || k.DESTINATION_TABLE || '
                     SET TOTAL_COUNT = NVL(TOTAL_COUNT,0) + 1,
                         COUNT_BEYOND_LCL_MIN =
                             CASE WHEN :1 < :2
                                  THEN NVL(COUNT_BEYOND_LCL_MIN,0) + 1
                                  ELSE COUNT_BEYOND_LCL_MIN END,
                         COUNT_BEYOND_UCL_MAX =
                             CASE WHEN :1 > :3
                                  THEN NVL(COUNT_BEYOND_UCL_MAX,0) + 1
                                  ELSE COUNT_BEYOND_UCL_MAX END
                     WHERE DATE_TIME = :4
                       AND PLANT = :5
                       AND COLUMN_NAME = :6';

                EXECUTE IMMEDIATE vSql
                    USING vValue,
                          k.LCL,
                          k.UCL,
                          vMAXDATE,
                          k.PLANT,
                          k.COLUMN_NAME;
            END IF;

        EXCEPTION
            WHEN OTHERS THEN
                DBMS_OUTPUT.PUT_LINE(
                    'ERROR SL_NO=' || k.SL_NO || ' : ' || SQLERRM
                );
        END;
    END LOOP;

    COMMIT;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('PROC ERROR: ' || SQLERRM);
END PROC_TSM_DRI_ALERT;
/