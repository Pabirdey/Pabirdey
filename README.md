 
            SELECT b.TAG_ID,b.WEB_COLUMN MATERIAL_NAME,
            CASE 
            WHEN b.FUR_NAME IN('C','E','F') THEN Round(NVL(a.VALUE,0) / 1000,2) END AS VALUE_TON,
            CASE
            WHEN  CASE WHEN b.FUR_NAME IN('C','E','F') THEN Round(NVL(a.VALUE,0),2)  END AS VALUE_KG            
            FROM imtg.T_ATOF_BIN_DETAILS b ,TEST.T_FURNACES_PROC_HM_PROD a Where b.TAG_ID = a.TAG_ID(+)
            AND b.REQUIRED = 'Y' AND b.WEB_COLUMN IS NOT NULL AND a.TIMESTAMP(+) =p_date AND b.FUR_NAME =p_furnace
            ORDER BY WEB_SL_NO;  
