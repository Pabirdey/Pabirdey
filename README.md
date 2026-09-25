CREATE OR REPLACE PROCEDURE PROC_TSM_SP1_PROD_DAILY
AS
    vMaxdate   DATE;
    v_Sql      VARCHAR2(32667);

BEGIN

    -- =========================================================
    -- STEP 1 : GET LAST PROCESSED DATE
    -- =========================================================

    SELECT MAX(TIMESTAMP) - 7
    INTO vMaxdate
    FROM TEST.T_TSBSL_SN_PROD_DAILY
    WHERE SOURCE = 'SP1';


    -- =========================================================
    -- STEP 2 : FIRST TIME EXECUTION
    -- =========================================================

    IF vMaxdate IS NULL THEN

        vMaxdate := TO_DATE(
                        '01-APR-2026',
                        'DD-MON-YYYY'
                    );

    END IF;


    -- =========================================================
    -- STEP 3 : TAG MASTER LOOP
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
            -- STEP 4 : RAW DATA LOOP
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
                    -- STEP 5 :
                    -- MERGE ONLY SOURCE + TIMESTAMP
                    -- =========================================

                    v_Sql :=
                        'MERGE INTO TEST.T_TSBSL_SN_PROD_DAILY D
                         USING
                         (
                             SELECT
                                 :1 AS SOURCE,
                                 :2 AS TIMESTAMP
                             FROM DUAL
                         ) S
                         ON
                         (
                             D.SOURCE = S.SOURCE
                             AND D.TIMESTAMP = S.TIMESTAMP
                         )
                         WHEN NOT MATCHED THEN
                             INSERT
                             (
                                 SOURCE,
                                 TIMESTAMP
                             )
                             VALUES
                             (
                                 S.SOURCE,
                                 S.TIMESTAMP
                             )';


                    EXECUTE IMMEDIATE v_Sql
                        USING
                            'SP1',
                            t.DATE_TIME;


                    -- =========================================
                    -- STEP 6 :
                    -- UPDATE DYNAMIC DESTINATION COLUMN
                    -- =========================================

                    v_Sql :=
                        'UPDATE TEST.T_TSBSL_SN_PROD_DAILY
                         SET ' || k.DEST_COLUMN || ' = :1
                         WHERE SOURCE = :2
                           AND TIMESTAMP = :3';


                    EXECUTE IMMEDIATE v_Sql
                        USING
                            t.COLUMN_VALUE,
                            'SP1',
                            t.DATE_TIME;


                EXCEPTION

                    WHEN OTHERS THEN

                        DBMS_OUTPUT.PUT_LINE(
                            '-----------------------------------'
                        );

                        DBMS_OUTPUT.PUT_LINE(
                            'SL_NO       : ' || k.SL_NO
                        );

                        DBMS_OUTPUT.PUT_LINE(
                            'DEST_COLUMN : ' || k.DEST_COLUMN
                        );

                        DBMS_OUTPUT.PUT_LINE(
                            'DATE_TIME   : ' || t.DATE_TIME
                        );

                        DBMS_OUTPUT.PUT_LINE(
                            'ERROR       : ' || SQLERRM
                        );

                        DBMS_OUTPUT.PUT_LINE(
                            '-----------------------------------'
                        );

                END;

            END LOOP;


        EXCEPTION

            WHEN OTHERS THEN

                DBMS_OUTPUT.PUT_LINE(
                    'TAG MASTER ERROR'
                );

                DBMS_OUTPUT.PUT_LINE(
                    'SL_NO = ' || k.SL_NO
                );

                DBMS_OUTPUT.PUT_LINE(
                    'DEST_COLUMN = ' || k.DEST_COLUMN
                );

                DBMS_OUTPUT.PUT_LINE(
                    'ERROR = ' || SQLERRM
                );

        END;

    END LOOP;


    -- =========================================================
    -- STEP 7 : COMMIT
    -- =========================================================

    COMMIT;


EXCEPTION

    WHEN OTHERS THEN

        ROLLBACK;

        DBMS_OUTPUT.PUT_LINE(
            'MAIN PROCEDURE ERROR = ' || SQLERRM
        );

END;
/