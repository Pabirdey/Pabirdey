UPDATE imtg.T_JODA_WET_PLANT_PROD_DAILY m
SET (
    RH_PRM_C1,
    RH_PRM_AF2,
    SEC_RH_AF3,
    SEC_TON_C8,
    SEC_TON_C10,
    HYDRO_TON_C9,
    NDCMP_PCH_RUN_HOUR,
    NDCMP_AF1_RUN_HOUR,
    NDCMP_AF3_RUN_HR,
    "500TPH_NBF1_RUN_HOURS",
    AF2_RUN_HR,
    NDCMP_DPC4_RUN_HOUR
) = (
    SELECT 
        (a.RH_PRM_C1 - b.RH_PRM_C1),
        (a.RH_PRM_AF2 - b.RH_PRM_AF2),
        (a.SEC_RH_AF3 - b.SEC_RH_AF3),
        (a.SEC_TON_C8 - b.SEC_TON_C8),
        (a.SEC_TON_C10 - b.SEC_TON_C10),
        (a.HYDRO_TON_C9 - b.HYDRO_TON_C9),
        (a.NDCMP_PCH_RUN_HOUR - b.NDCMP_PCH_RUN_HOUR),
        (a.NDCMP_AF1_RUN_HOUR - b.NDCMP_AF1_RUN_HOUR),
        (a.NDCMP_AF3_RUN_HR - b.NDCMP_AF3_RUN_HR),
        (a."500TPH_NBF1_RUN_HOURS" - b."500TPH_NBF1_RUN_HOURS"),
        (a.AF2_RUN_HR - b.AF2_RUN_HR),
        (a.NDCMP_DPC4_RUN_HOUR - b.NDCMP_DPC4_RUN_HOUR)
    FROM IMTG.T_JODA_WET_PLANT_PROD_DAILY a
    JOIN IMTG.T_JODA_WET_PLANT_PROD_DAILY b
      ON a.Timestamp - 1 = b.Timestamp
    WHERE a.Timestamp = m.Timestamp
)
WHERE m.Timestamp >= SYSDATE - 200;

COMMIT;
