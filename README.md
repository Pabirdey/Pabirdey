CREATE OR REPLACE PROCEDURE PROC_TSM_DRI_ALERT
AS
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
        vMAXDATE := TO_DATE('01-JAN-2026','DD-MON-YYYY');
    END IF;

    vSTDATE := vMAXDATE;
    vTODATE := SYSDATE;

    /* Loop master table */
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
            /* Check destination row */
            SELECT COUNT(*)
            INTO vCount
            FROM TSBSL.T_TSM_DRI_ALERT
            WHERE DATE_TIME = vMAXDATE
              AND PLANT = k.PLANT
              AND COLUMN_NAME = k.COLUMN_NAME;

            IF vCount = 0 THEN
                INSERT INTO TSBSL.T_TSM_DRI_ALERT
                (DATE_TIME, PLANT, COLUMN_NAME,
                 TOTAL_COUNT, COUNT_BEYOND_LCL_MIN, COUNT_BEYOND_UCL_MAX)
                VALUES
                (vMAXDATE, k.PLANT, k.COLUMN_NAME, 0, 0, 0);
            END IF;

            /* -------- Dynamic SELECT (NO BINDS) -------- */
            vSql :=
                'SELECT ' || k.COLUMN_NAME ||
                ' FROM ' || k.SOURCE_TABLE ||
                ' WHERE DATE_TIME >= TO_DATE(''' ||
                TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                ''',''DD-MON-YYYY HH24:MI:SS'')' ||
                ' AND DATE_TIME <= TO_DATE(''' ||
                TO_CHAR(vTODATE,'DD-MON-YYYY HH24:MI:SS') ||
                ''',''DD-MON-YYYY HH24:MI:SS'')' ||
                ' AND PLANT = ''' || k.PLANT || '''';

            EXECUTE IMMEDIATE vSql INTO vValue;

            /* -------- Alert logic -------- */
            IF vValue < k.LCL THEN

                vSql :=
                    'UPDATE ' || k.DESTINATION_TABLE ||
                    ' SET TOTAL_COUNT = NVL(TOTAL_COUNT,0) + 1,
                          COUNT_BEYOND_LCL_MIN = NVL(COUNT_BEYOND_LCL_MIN,0) + 1
                      WHERE DATE_TIME = TO_DATE(''' ||
                    TO_CHAR(vMAXDATE,'DD-MON-YYYY HH24:MI:SS') ||
                    ''',''DD-MON-YYYY HH24:MI:SS'')
                        AND PLANT = ''' || k.PLANT || '''
                        AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';

                EXECUTE IMMEDIATE vSql;

            ELSIF vValue > k.UCL THEN

                vSql :=
                    'UPDATE ' || k.DESTINATION_TABLE ||
                    ' SET TOTAL_COUNT = NVL(TOTAL_COUNT,0) + 1,
                          COUNT_BEYOND_UCL_MAX = NVL(COUNT_BEYOND_UCL_MAX,0) + 1
                      WHERE DATE_TIME = TO_DATE(''' ||
                    TO_CHAR(vMAXDATE,'DD-MON-YYYY HH24:MI:SS') ||
                    ''',''DD-MON-YYYY HH24:MI:SS'')
                        AND PLANT = ''' || k.PLANT || '''
                        AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';

                EXECUTE IMMEDIATE vSql;
            END IF;

        EXCEPTION
            WHEN NO_DATA_FOUND THEN
                NULL;
            WHEN TOO_MANY_ROWS THEN
                DBMS_OUTPUT.PUT_LINE(
                    'Multiple rows found for ' || k.COLUMN_NAME
                );
            WHEN OTHERS THEN
                DBMS_OUTPUT.PUT_LINE(
                    'ERROR SL_NO=' || k.SL_NO || ' : ' || SQLERRM
                );
        END;
    END LOOP;

    COMMIT;
END PROC_TSM_DRI_ALERT;
/