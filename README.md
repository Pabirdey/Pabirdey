SELECT 
                        NVL(SUM(CASE WHEN DESTINATION = 'LD1' THEN NET_WT END), 0) AS LD1_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD2' THEN NET_WT END), 0) AS LD2_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'LD3' THEN NET_WT END), 0) AS LD3_TONS,
                        NVL(SUM(CASE WHEN DESTINATION = 'MRD' AND TRP_NO <= 50 THEN NET_WT END), 0) AS MRDTP_TONS,
                        NVL(SUM(CASE WHEN TRP_NO <= 50 AND RET_FLAG = 'N' THEN FILL_STATUS END), 0) AS NOOFTP,                       
                    FROM demo.t_ladle_details
                    WHERE LADLE_FLEND_TIME >= TO_DATE(:pDate,'DD/MM/YYYY') + 6/24
                      AND LADLE_FLEND_TIME <  TO_DATE(:pDate,'DD/MM/YYYY') + 1 + 6/24
                      AND FUR_NAME IN ('G')";
