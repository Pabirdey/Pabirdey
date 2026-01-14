CREATE OR REPLACE PROCEDURE PROC_TSM_DRI_ALERT_UPDATE AS

    v_sql        CLOB;
    v_value      NUMBER;

BEGIN
    FOR rec IN (
        SELECT COLUMN_NAME,
               SOURCE_TABLE,
               DESTINATION_TABLE,
               LCL,
               UCL,
               PLANT,
               SOURCE
        FROM TSBSL.T_TSM_DRI_ALERT_CONFIG
    )
    LOOP
        /* 1️⃣ Read value dynamically from source table */
        v_sql :=
            'SELECT ' || rec.COLUMN_NAME ||
            ' FROM ' || rec.SOURCE_TABLE ||
            ' WHERE PLANT = :1';

        EXECUTE IMMEDIATE v_sql
        INTO v_value
        USING rec.PLANT;

        /* 2️⃣ Check limit */
        IF v_value < rec.LCL OR v_value > rec.UCL THEN

            /* 3️⃣ Update destination table dynamically */
            v_sql :=
                'UPDATE ' || rec.DESTINATION_TABLE || '
                 SET ACTUAL_VALUE = :1,
                     ALERT_STATUS = ''Y'',
                     ALERT_DATE = SYSDATE
                 WHERE PLANT = :2
                   AND TAG_NAME = :3';

            EXECUTE IMMEDIATE v_sql
            USING v_value, rec.PLANT, rec.COLUMN_NAME;

        END IF;

    END LOOP;

    COMMIT;

END PROC_TSM_DRI_ALERT_UPDATE;
/