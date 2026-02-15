    CASE 
        WHEN b.FUR_NAME IN ('C','E','F') 
        THEN ROUND(NVL(a.VALUE,0) / 1000,2)
        ELSE 0
    END AS VALUE_TON,

    CASE 
        WHEN b.FUR_NAME IN ('C','E','F') 
        THEN ROUND(NVL(a.VALUE,0),2)
        ELSE 0
    END AS VALUE_KG
