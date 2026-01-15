-- LCL COUNT
vSql :=
    'SELECT COUNT(*) FROM ' || k.SOURCE_TABLE ||
    ' WHERE DATE_TIME >= TO_DATE(''' || TO_CHAR(vSTDATE,'DD-MON-YYYY HH24:MI:SS') || ''',''DD-MON-YYYY HH24:MI:SS'')' ||
    ' AND DATE_TIME <= TO_DATE(''' || TO_CHAR(vTODATE,'DD-MON-YYYY HH24:MI:SS') || ''',''DD-MON-YYYY HH24:MI:SS'')' ||
    ' AND PLANT = ''' || k.PLANT || '''' ||
    ' AND ' || k.COLUMN_NAME || ' < ' || k.LCL;

EXECUTE IMMEDIATE vSql INTO vValue;

IF vValue > 0 THEN
    EXECUTE IMMEDIATE
    'UPDATE ' || k.DESTINATION_TABLE ||
    ' SET COUNT_BEYOND_LCL_MIN = NVL(COUNT_BEYOND_LCL_MIN,0) + ' || vValue ||
    ' WHERE DATE_TIME = TO_DATE(''' || TO_CHAR(vMAXDATE,'DD-MON-YYYY HH24:MI:SS') ||
    ''',''DD-MON-YYYY HH24:MI:SS'')' ||
    ' AND PLANT = ''' || k.PLANT || '''' ||
    ' AND COLUMN_NAME = ''' || k.COLUMN_NAME || '''';
END IF;