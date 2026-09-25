CREATE OR REPLACE PROCEDURE PROC_TSM_SP1_PROD_DAILY
AS
    vMaxdate       DATE;
    v_Sql          VARCHAR2(32667);
    vCount         NUMBER;
BEGIN

    -- Date format
    EXECUTE IMMEDIATE
        'ALTER SESSION SET NLS_DATE_FORMAT = ''DD-MON-YYYY HH24:MI:SS''';

    -- Get last processed date
    SELECT MAX(TIMESTAMP) - 7
    INTO vMaxdate
    FROM TEST.T_TSBSL_SN_PROD_DAILY
    WHERE SOURCE = 'SP1';

    -- First time execution
    IF vMaxdate IS NULL THEN
        vMaxdate := TO_DATE('01-APR-2026', 'DD-MON-YYYY');
    END IF;


    -- =========================================================
    -- TAG MASTER LOOP
    -- =========================================================
    FOR k IN
    (
        SELECT
            SL_NO,
            SOURCE_TABLE,
            DESTINATION_TABLE,
            DEST_COLUMN,
            FREQUENCY
        FROM TEST.T_TSM_SP1_PROD_TAG_MASTER
        WHERE SOURCE = 'SP1'
          AND REQUIRED = 'Y'
        ORDER BY SL_NO
    )
    LOOP

        BEGIN

            -- =================================================
            -- RAW DATA LOOP
            -- =================================================
            FOR t IN
            (
                SELECT
                    SL_NO,
                    DATE_TIME,
                    FREQUENCY,
                    COLUMN_NAME,
                    COLUMN_VALUE
                FROM TEST.T_TSM_SP1_PROD_RAW
                WHERE DATE_TIME >= vMaxdate
                  AND COLUMN_NAME = k.DEST_COLUMN
                  AND FREQUENCY = k.FREQUENCY
                  AND SL_NO = k.SL_NO
                ORDER BY DATE_TIME
            )
            LOOP

                BEGIN

                    -- =========================================
                    -- CHECK TIMESTAMP ALREADY EXISTS
                    -- =========================================
                    SELECT COUNT(*)
                    INTO vCount
                    FROM TEST.T_TSBSL_SN_PROD_DAILY
                    WHERE SOURCE = 'SP1'
                      AND TIMESTAMP = t.DATE_TIME;


                    -- =========================================
                    -- IF TIMESTAMP DOES NOT EXIST
                    -- INSERT NEW ROW
                    -- =========================================
                    IF vCount = 0 THEN

                        v_Sql :=
                            'INSERT INTO TEST.T_TSBSL_SN_PROD_DAILY
                             (SOURCE, TIMESTAMP)
                             VALUES
                             (:1, :2)';

                        EXECUTE IMMEDIATE v_Sql
                            USING 'SP1', t.DATE_TIME;

                    END IF;


                    -- =========================================
                    -- UPDATE DYNAMIC DESTINATION COLUMN
                    -- =========================================

                    v_Sql :=
                        'UPDATE TEST.T_TSBSL_SN_PROD_DAILY
                         SET ' || k.DEST_COLUMN || ' = :1
                         WHERE SOURCE = :2
                           AND TIMESTAMP = :3';

                    EXECUTE IMMEDIATE v_Sql
                        USING t.COLUMN_VALUE,
                              'SP1',
                              t.DATE_TIME;


                EXCEPTION
                    WHEN OTHERS THEN
                        DBMS_OUTPUT.PUT_LINE(
                            'SL_NO=' || k.SL_NO ||
                            ', COLUMN=' || k.DEST_COLUMN ||
                            ', DATE=' || t.DATE_TIME ||
                            ', ERROR=' || SQLERRM
                        );
                END;

            END LOOP;


        EXCEPTION
            WHEN OTHERS THEN
                DBMS_OUTPUT.PUT_LINE(
                    'TAG SL_NO=' || k.SL_NO ||
                    ', ERROR=' || SQLERRM
                );
        END;

    END LOOP;


    COMMIT;


EXCEPTION
    WHEN OTHERS THEN
        ROLLBACK;

        DBMS_OUTPUT.PUT_LINE(
            'MAIN ERROR: ' || SQLERRM
        );

END;
/