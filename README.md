CREATE OR REPLACE PROCEDURE PROC_TMET_RAW_DATA IS

    vTimestamp      DATE;
    vMaxTimestamp   DATE;

    vSQL_TIME       VARCHAR2(32666);
    vSQL_COL        VARCHAR2(32666);
    vSQL_VAL        VARCHAR2(32666);
    vSQL_DATA       VARCHAR2(32666);
    vSQL_COUNT      VARCHAR2(32666);

    vCount          NUMBER(5);
    vTABLE_NAME     VARCHAR2(100);

    -- ==========================================
    -- SAFE PRINT
    -- ==========================================
    PROCEDURE PRINT_LONG(p_text VARCHAR2) IS
        v_pos NUMBER := 1;
        v_len NUMBER;
    BEGIN

        IF p_text IS NULL THEN
            DBMS_OUTPUT.PUT_LINE('NULL');
            RETURN;
        END IF;

        v_len := LENGTH(p_text);

        WHILE v_pos <= v_len LOOP

            DBMS_OUTPUT.PUT_LINE(
                SUBSTR(p_text, v_pos, 250)
            );

            v_pos := v_pos + 250;

        END LOOP;

    END PRINT_LONG;


BEGIN

    DBMS_OUTPUT.ENABLE(1000000);

    vTABLE_NAME := NULL;

    EXECUTE IMMEDIATE
        'ALTER SESSION SET NLS_DATE_FORMAT=''DD-MON-YYYY HH24:MI:SS''';


    FOR i IN
    (
        SELECT DISTINCT
               DESTINATION_TABLE,
               PLANT,
               FREQUENCY
        FROM TMET.T_TMET_L2_TAG_MASTER
    )
    LOOP

        BEGIN

            vMaxTimestamp := NULL;

            vSQL_TIME :=
                'SELECT MAX(TIMESTAMP)-1/24 FROM '
                || i.DESTINATION_TABLE;

            EXECUTE IMMEDIATE
                vSQL_TIME
                INTO vMaxTimestamp;


            IF vMaxTimestamp IS NULL THEN

                vMaxTimestamp :=
                    '11-NOV-2025 17:00:00';

            END IF;


            IF vTABLE_NAME IS NULL
               OR vTABLE_NAME <> i.DESTINATION_TABLE
            THEN

                vTimestamp := vMaxTimestamp;

                LOOP

                    EXIT WHEN
                        vTimestamp >= SYSDATE - 6/288;

                    vSQL_COUNT := NULL;
                    vCount := NULL;

                    /*
                       Your existing vSQL_COUNT
                       construction here
                    */

                    -- Your existing processing

                END LOOP;

            END IF;


            /*
             * Your existing vSQL_COL
             * and vSQL_VAL construction
             */

            vSQL_COL :=
                SUBSTR(
                    vSQL_COL,
                    0,
                    LENGTH(vSQL_COL) - 1
                ) || ') = (';

            vSQL_VAL :=
                SUBSTR(
                    vSQL_VAL,
                    0,
                    LENGTH(vSQL_VAL) - 1
                );

            vSQL_DATA :=
                vSQL_COL || vSQL_VAL;


            -- =========================================
            -- IMPORTANT: DO NOT USE PUT_LINE DIRECTLY
            -- =========================================

            PRINT_LONG(vSQL_DATA);


            EXECUTE IMMEDIATE vSQL_DATA;

            COMMIT;

        EXCEPTION
            WHEN OTHERS THEN

                PRINT_LONG(
                    i.DESTINATION_TABLE ||
                    ' - ' ||
                    SQLERRM
                );

        END;

    END LOOP;

END PROC_TMET_RAW_DATA;
/