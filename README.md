CREATE OR REPLACE PROCEDURE PROC_TSM_DRI_DELAY_DAILY AS

    v_curr_date DATE;

BEGIN
    EXECUTE IMMEDIATE
        'ALTER SESSION SET NLS_DATE_FORMAT = ''DD-MON-YYYY HH24:MI:SS''';

    FOR k IN (
        SELECT START_TIMESTAMP,
               END_TIMESTAMP,
               PLANT,
               AGENCY
        FROM TSBSL.T_TSM_DRI_DELAYS
        WHERE START_TIMESTAMP >= DATE '2025-11-01'
          AND END_TIMESTAMP   <= DATE '2025-12-01'
        ORDER BY PLANT, AGENCY, START_TIMESTAMP
    )
    LOOP
        -- start date
        v_curr_date := TRUNC(k.START_TIMESTAMP);

        -- loop for each day
        WHILE v_curr_date <= TRUNC(k.END_TIMESTAMP)
        LOOP
            BEGIN
                INSERT INTO TSBSL.T_TSM_DRI_DELAYS_DAILY
                (
                    DATE_TIME,
                    PLANT,
                    AGENCY
                )
                VALUES
                (
                    v_curr_date,
                    k.PLANT,
                    k.AGENCY
                );

            EXCEPTION
                WHEN DUP_VAL_ON_INDEX THEN
                    NULL; -- skip existing day
                WHEN OTHERS THEN
                    DBMS_OUTPUT.PUT_LINE(
                        'Insert Error [' || k.PLANT || ' - ' || k.AGENCY || '] : ' || SQLERRM
                    );
            END;

            v_curr_date := v_curr_date + 1;
        END LOOP;

    END LOOP;

    COMMIT;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('General Error: ' || SQLERRM);
END;
/