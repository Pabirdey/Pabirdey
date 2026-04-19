SELECT 
    NVL(SUM(CASE WHEN a.DESTINATION = 'LD1' THEN a.NET_WT END), 0) AS LD1_TONS,
     NVL(SUM(CASE WHEN DESTINATION = 'LD2' THEN NET_WT END), 0) AS LD2_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD3' THEN NET_WT END), 0) AS LD3_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'MRD' AND TRP_NO <= 50 THEN NET_WT END), 0) AS MRDTP_TONS,
                        NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END), 0) AS NOOFTP,
    NVL((
        SELECT SUM(CASE WHEN b.DESTINATION = 'LD1' THEN b.NET_WT END)
        FROM demo.t_ladle b
        WHERE b.FUR_NAME = a.FUR_NAME
          AND b.DATE_TIME >= TRUNC(TO_DATE(:pDate,'DD/MM/YYYY'),'MON') + 6/24
          AND b.DATE_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
    ), 0) AS LD1_TONS_ACTUAL,
    NVL((
        SELECT SUM(CASE WHEN b.DESTINATION = 'LD2' THEN b.NET_WT END)
        FROM demo.t_ladle b
        WHERE b.FUR_NAME = a.FUR_NAME
          AND b.DATE_TIME >= TRUNC(TO_DATE(:pDate,'DD/MM/YYYY'),'MON') + 6/24
          AND b.DATE_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
    ), 0) AS LD2_TONS_ACTUAL,
     NVL((
        SELECT SUM(CASE WHEN b.DESTINATION = 'LD3' THEN b.NET_WT END)
        FROM demo.t_ladle b
        WHERE b.FUR_NAME = a.FUR_NAME
          AND b.DATE_TIME >= TRUNC(TO_DATE(:pDate,'DD/MM/YYYY'),'MON') + 6/24
          AND b.DATE_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
    ), 0) AS LD3_TONS_ACTUAL,
NVL((
        SELECT SUM(CASE WHEN DESTINATION = 'MRD' AND TRP_NO <= 50 THEN NET_WT END)
        FROM demo.t_ladle b
        WHERE b.FUR_NAME = a.FUR_NAME
          AND b.DATE_TIME >= TRUNC(TO_DATE(:pDate,'DD/MM/YYYY'),'MON') + 6/24
          AND b.DATE_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
    ), 0) AS MRDTP_TONS_ACTUAL
FROM demo.t_ladle a
WHERE a.DATE_TIME >= TO_DATE(:pDate,'DD/MM/YYYY') + 6/24
  AND a.DATE_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
  AND a.FUR_NAME = 'G'
GROUP BY a.FUR_NAME;
