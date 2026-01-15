CREATE OR REPLACE PROCEDURE PROC_TSM_DRI_ALERT AS

    vSTDATE   DATE;
    vTODATE   DATE;

    vCount    NUMBER;
    vValue    NUMBER;

    vSql      VARCHAR2(32667);

BEGIN
    ----------------------------------------------------
    -- YOUR DATE RANGE
    ----------------------------------------------------
    vSTDATE := TO_DATE('01-JAN-2026','DD-MON-YYYY');
    vTODATE := TO_DATE('15-JAN-2026','DD-MON-YYYY');

    ----------------------------------------------------
    -- LOOP DAY BY DAY
    ----------------------------------------------------
    WHILE vSTDATE <= vTODATE
    LOOP

        ------------------------------------------------
        -- MASTER CONFIG LOOP
        ------------------------------------------------
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

            ------------------------------------------------
            -- CHECK RECORD EXIST
            ------------------------------------------------
            SELECT COUNT(*)
            INTO vCount
            FROM TSBSL.T_TSM_DRI_ALERT
            WHERE DATE_TIME = vSTDATE
              AND PLANT = k.PLANT
              AND COLUMN_NAME = k.COLUMN_NAME;

            IF vCount = 0 THEN
                INSERT INTO TSBSL.T_TSM_DRI_ALERT
                (
                    DATE_TIME,
                    PLANT,
                    COLUMN_NAME,
                    TOTAL_COUNT,
                    COUNT_BEYOND_LCL_MIN,
                    COUNT_BEYOND_UCL_MAX
                )
                VALUES
                (
                    vSTDATE,
                    k.PLANT,
                    k.COLUMN_NAME,
                    0,
                    0,
                    0
                );
            END IF;

            ------------------------------------------------
            -- LCL COUNT
            ------------------------------------------------
            vSql :=
            'SELECT COUNT(*) FROM ' || k.SOURCE_TABLE ||
            ' WHERE TRUNC(TIMESTAMP) = TO_DATE(''' ||
                TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                ''',''DD-MON-YYYY HH24:MI:SS'')' ||

            ' AND ' || k.COLUMN_NAME || ' < ' || k.LCL;

            EXECUTE IMMEDIATE vSql INTO vValue;

            IF vValue > 0 THEN
                EXECUTE IMMEDIATE
                'UPDATE ' || k.DESTINATION_TABLE ||
                ' SET COUNT_BEYOND_LCL_MIN = NVL(COUNT_BEYOND_LCL_MIN,0) + ' || vValue ||

                ' WHERE DATE_TIME = TO_DATE(''' ||
                    TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                    ''',''DD-MON-YYYY HH24:MI:SS'')' ||

                ' AND PLANT = ''' || k.PLANT || '''' ||
                ' AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';
            END IF;

            ------------------------------------------------
            -- UCL COUNT
            ------------------------------------------------
            vSql :=
            'SELECT COUNT(*) FROM ' || k.SOURCE_TABLE ||
            ' WHERE TRUNC(TIMESTAMP) = TO_DATE(''' ||
                TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                ''',''DD-MON-YYYY HH24:MI:SS'')' ||

            ' AND ' || k.COLUMN_NAME || ' > ' || k.UCL;

            EXECUTE IMMEDIATE vSql INTO vValue;

            IF vValue > 0 THEN
                EXECUTE IMMEDIATE
                'UPDATE ' || k.DESTINATION_TABLE ||
                ' SET COUNT_BEYOND_UCL_MAX = NVL(COUNT_BEYOND_UCL_MAX,0) + ' || vValue ||

                ' WHERE DATE_TIME = TO_DATE(''' ||
                    TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                    ''',''DD-MON-YYYY HH24:MI:SS'')' ||

                ' AND PLANT = ''' || k.PLANT || '''' ||
                ' AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';
            END IF;

            ------------------------------------------------
            -- ✅ TOTAL COUNT = LCL + UCL
            ------------------------------------------------
            EXECUTE IMMEDIATE
            'UPDATE ' || k.DESTINATION_TABLE || '
               SET TOTAL_COUNT =
                   NVL(COUNT_BEYOND_LCL_MIN,0) +
                   NVL(COUNT_BEYOND_UCL_MAX,0)

             WHERE DATE_TIME = TO_DATE(''' ||
                   TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
                   ''',''DD-MON-YYYY HH24:MI:SS'')' ||

            ' AND PLANT = ''' || k.PLANT || '''' ||
            ' AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';

        EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE(
                'ERROR IN SL_NO=' || k.SL_NO ||
                ' DATE=' || TO_CHAR(vSTDATE,'DD-MON-YYYY') ||
                ' : ' || SQLERRM
            );
        END;

        END LOOP;

        ------------------------------------------------
        -- NEXT DAY
        ------------------------------------------------
        vSTDATE := vSTDATE + 1;

    END LOOP;

    COMMIT;

END PROC_TSM_DRI_ALERT;
/