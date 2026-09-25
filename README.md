CREATE OR REPLACE PROCEDURE PROC_TSM_SP1_PROD_DAILY
AS
    vMaxdate   DATE;
    v_Sql      VARCHAR2(32667);
BEGIN

    -- =========================================================
    -- NLS DATE FORMAT
    -- =========================================================
    EXECUTE IMMEDIATE
        'ALTER SESSION SET NLS_DATE_FORMAT = ''DD-MON-YYYY HH24:MI:SS''';


    -- =========================================================
    -- GET LAST PROCESSED DATE
    -- =========================================================
    SELECT MAX(TIMESTAMP) - 7
    INTO vMaxdate
    FROM TEST.T_TSBSL_SN_PROD_DAILY
    WHERE SOURCE = 'SP1';


    -- =========================================================
    -- FIRST TIME EXECUTION
    -- =========================================================
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
                    -- DYNAMIC MERGE
                    -- =========================================

                    v_Sql :=
                        'MERGE INTO TEST.T_TSBSL_SN_PROD_DAILY d
                         USING
                         (
                             SELECT
                                 :1 AS SOURCE,
                                 :2 AS TIMESTAMP,
                                 :3 AS COLUMN_VALUE
                             FROM DUAL
                         ) s
                         ON
                         (
                             d.SOURCE = s.SOURCE
                             AND d.TIMESTAMP = s.TIMESTAMP
                         )
                         WHEN MATCHED THEN
                             UPDATE SET d.' || k.DEST_COLUMN || ' = s.COLUMN_VALUE
                         WHEN NOT MATCHED THEN
                             INSERT
                             (
                                 SOURCE,
                                 TIMESTAMP,
                                 ' || k.DEST_COLUMN || '
                             )
                             VALUES
                             (
                                 s.SOURCE,
                                 s.TIMESTAMP,
                                 s.COLUMN_VALUE
                             )';


                    EXECUTE IMMEDIATE v_Sql
                        USING
                            'SP1',
                            t.DATE_TIME,
                            t.COLUMN_VALUE;


                EXCEPTION
                    WHEN OTHERS THEN

                        DBMS_OUTPUT.PUT_LINE(
                            'SL_NO = ' || k.SL_NO ||
                            ' | COLUMN = ' || k.DEST_COLUMN ||
                            ' | DATE = ' || t.DATE_TIME ||
                            ' | ERROR = ' || SQLERRM
                        );

                END;

            END LOOP;


        EXCEPTION
            WHEN OTHERS THEN

                DBMS_OUTPUT.PUT_LINE(
                    'TAG SL_NO = ' || k.SL_NO ||
                    ' | ERROR = ' || SQLERRM
                );

        END;

    END LOOP;


    -- =========================================================
    -- COMMIT
    -- =========================================================
    COMMIT;


EXCEPTION
    WHEN OTHERS THEN

        ROLLBACK;

        DBMS_OUTPUT.PUT_LINE(
            'MAIN ERROR = ' || SQLERRM
        );

END;
/