k.SOURCE = 'QUALITY' AND k.TAG_DECRIPTION = 'Feed coal FC' THEN
BEGIN

    -- ===== LCL COUNT =====
    vSql :=
    'SELECT COUNT(*) FROM ' || k.SOURCE_TABLE ||
    ' WHERE TRUNC(TIMESTAMP) = TO_DATE(''' ||
        TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
    ''',''DD-MON-YYYY HH24:MI:SS'')' ||
    ' AND ' || k.COLUMN_NAME || ' < ' || k.LCL ||
    ' AND ' || k.SOURCE || ' = ''FEED COAL FOR DRI''';

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


    -- ===== UCL COUNT =====
    vSql :=
    'SELECT COUNT(*) FROM ' || k.SOURCE_TABLE ||
    ' WHERE TRUNC(TIMESTAMP) = TO_DATE(''' ||
        TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') ||
    ''',''DD-MON-YYYY HH24:MI:SS'')' ||
    ' AND ' || k.COLUMN_NAME || ' > ' || k.UCL ||
    ' AND ' || k.SOURCE || ' = ''FEED COAL FOR DRI''';

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


    -- ===== TOTAL =====
    EXECUTE IMMEDIATE
    'UPDATE ' || k.DESTINATION_TABLE ||
    ' SET TOTAL_COUNT = NVL(COUNT_BEYOND_LCL_MIN,0) + NVL(COUNT_BEYOND_UCL_MAX,0)' ||
    ' WHERE DATE_TIME = TO_DATE(''' ||
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