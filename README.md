SELECT  NVL(SUM(CASE  WHEN DESTINATION='LD1' THEN NET_WT ELSE 0 END),0) LD1,
                                                           NVL(SUM(CASE  WHEN DESTINATION='LD2' THEN NET_WT ELSE 0 END),0) LD2,
                                                           NVL(SUM(CASE  WHEN DESTINATION='LD3' THEN NET_WT ELSE 0 END),0) LD3,
                                                           NVL(SUM(CASE  WHEN DESTINATION='MRD' THEN NET_WT ELSE 0 END),0) MRD,
                                                           NVL(SUM(CASE  WHEN TRP_NO<=50 AND RET_FLAG='N' THEN FILL_STATUS ELSE 0 END),0) NOOFTP
                                                           FROM DEMO.T_LADLE_DETAILS WHERE LADLE_FLEND_TIME >= :fromDate AND LADLE_FLEND_TIME < :toDate
                                                            AND fur_name = :furnace
