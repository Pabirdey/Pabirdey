create or replace Procedure Proc_Get_BF_Raw_Material(p_furnace IN VARCHAR2,p_date IN DATE,p_cursor OUT SYS_REFCURSOR)AS
Begin
OPEN p_cursor FOR
SELECT             
    b.WEB_COLUMN,    
    NVL(a.VALUE,0) AS VALUE,    
    /* Value Kgs */
    CASE 
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet' 
            THEN NVL(a.VALUE,0) * 1000
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0)
        ELSE NVL(a.VALUE,0)
    END AS VAL_KGS,

    /* Value Tons */
    CASE 
        WHEN b.FUR_NAME = 'F' AND b.WEB_COLUMN = 'Pellet'
            THEN NVL(a.VALUE,0)
        WHEN b.FUR_NAME = 'F'
            THEN NVL(a.VALUE,0) / 1000
        ELSE NVL(a.VALUE,0) / 1000
    END AS VAL_TONS

FROM T_ATOF_BIN_DETAILS b
LEFT JOIN t_furnaces_proc_hm_prod a
       ON b.TAG_ID = a.TAG_ID
WHERE b.REQUIRED = 'Y'
  AND b.WEB_COLUMN IS NOT NULL AND a.Timestamp=p_date AND b.FUR_NAME=p_furnace Order by WEB_SL_NO;

  IF SQL%ROWCOUNT=0 THEN
        OPEN p_cursor FOR
        Select WEB_COLUMN From imtg.T_ATOF_BIN_DETAILS Where Required='Y' AND WEB_COLUMN IS NOT NULL AND FUR_NAME=p_furnace Order by WEB_SL_NO;
  END IF; 

Exception
When Others Then 
DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
