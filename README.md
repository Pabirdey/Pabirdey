create or replace PROCEDURE Proc_Get_BF_Raw_Material(p_furnace IN VARCHAR2,p_date IN DATE,p_cursor OUT SYS_REFCURSOR)
AS
    v_count NUMBER;
Begin  
    Execute immediate 'Alter session set nls_date_format=''DD-MON-YYYY HH24:MI:SS''';
    SELECT COUNT(*) into v_count FROM TEST.T_FURNACES_PROC_HM_PROD a,imtg.T_ATOF_BIN_DETAILS b Where b.TAG_ID = a.TAG_ID
    AND b.REQUIRED = 'Y' AND b.WEB_COLUMN IS NOT NULL  AND a.TIMESTAMP = p_date AND b.FUR_NAME = p_furnace;    
    Begin  
        IF v_count > 0 THEN
            OPEN p_cursor FOR           
            SELECT b.TAG_ID,b.WEB_COLUMN MATERIAL_NAME,
            CASE WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' THEN Round(NVL(a.VALUE,0),2)
            WHEN b.FUR_NAME = 'F' THEN Round(NVL(a.VALUE,0) / 1000,2) ELSE Round(NVL(a.VALUE,0) / 1000,2) END AS VALUE_TON,
            CASE WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' THEN Round(NVL(a.VALUE,0) * 1000,2)
            WHEN b.FUR_NAME = 'F' THEN round(NVL(a.VALUE,0),2) ELSE Round(NVL(a.VALUE,0),2) END AS VALUE_KG            
            FROM imtg.T_ATOF_BIN_DETAILS b ,TEST.T_FURNACES_PROC_HM_PROD a Where b.TAG_ID = a.TAG_ID(+)
            AND b.REQUIRED = 'Y' AND b.WEB_COLUMN IS NOT NULL AND a.TIMESTAMP(+) =p_date AND b.FUR_NAME =p_furnace
            ORDER BY WEB_SL_NO;    
            
            
        ELSE
            OPEN p_cursor FOR
            SELECT TAG_ID,WEB_COLUMN MATERIAL_NAME,0 VALUE_TON,0 VALUE_KG FROM imtg.T_ATOF_BIN_DETAILS WHERE REQUIRED = 'Y' AND WEB_COLUMN IS NOT NULL AND FUR_NAME = p_furnace ORDER BY WEB_SL_NO;
        END IF;
    EXCEPTION
    WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE(SQLERRM);
    END;
EXCEPTION
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
