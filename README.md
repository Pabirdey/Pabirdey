BEGIN

FOR k IN (
    SELECT SAMPLE_DATE,
           PRODUCT,

           AVG(DECODE(PRODUCT,'SO',DECODE(DESTINATION,'TSBSL',QUANTITY))) QTY_TSM_SO,
           AVG(DECODE(PRODUCT,'BF',DECODE(DESTINATION,'TSBSL',QUANTITY))) QTY_TSM_BF,

           AVG(DECODE(PRODUCT,'SO',DECODE(DESTINATION,'TSBSL',AL2O3))) AL2O3_TSM_SO,
           AVG(DECODE(PRODUCT,'BF',DECODE(DESTINATION,'TSBSL',AL2O3))) AL2O3_TSM_BF,

           AVG(DECODE(PRODUCT,'SO',DECODE(DESTINATION,'TSBSL',K2O))) K2O_TSM_SO,
           AVG(DECODE(PRODUCT,'BF',DECODE(DESTINATION,'TSBSL',K2O))) K2O_TSM_BF,

           AVG(DECODE(PRODUCT,'SO',DECODE(DESTINATION,'TSBSL',FE))) FE_TSM_SO,
           AVG(DECODE(PRODUCT,'BF',DECODE(DESTINATION,'TSBSL',FE))) FE_TSM_BF,

           AVG(DECODE(PRODUCT,'SO',DECODE(DESTINATION,'TSBSL',PHOS))) PHOS_TSM_SO,
           AVG(DECODE(PRODUCT,'BF',DECODE(DESTINATION,'TSBSL',PHOS))) PHOS_TSM_BF

    FROM T_KHONDBOND_ORE
    WHERE SAMPLE_DATE >= v_STDATE
    GROUP BY SAMPLE_DATE, PRODUCT
)

LOOP

    BEGIN

        UPDATE imtg.T_RM_MIS_DAILY
        SET DESPATCH_IRON_ORE =
                DECODE(k.PRODUCT,
                       'SO', k.QTY_TSM_SO,
                       'BF', k.QTY_TSM_BF),

            DESPATCH_ALUMINA =
                DECODE(k.PRODUCT,
                       'SO', k.AL2O3_TSM_SO,
                       'BF', k.AL2O3_TSM_BF),

            ALKALI_K2O =
                DECODE(k.PRODUCT,
                       'SO', k.K2O_TSM_SO,
                       'BF', k.K2O_TSM_BF),

            FE =
                DECODE(k.PRODUCT,
                       'SO', k.FE_TSM_SO,
                       'BF', k.FE_TSM_BF),

            PHOS =
                DECODE(k.PRODUCT,
                       'SO', k.PHOS_TSM_SO,
                       'BF', k.PHOS_TSM_BF)

        WHERE TIMESTAMP = k.SAMPLE_DATE
        AND PLANT = 'TSM'
        AND PRODUCT = k.PRODUCT;   -- ✅ Important Fix

    EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE(SQLERRM);
    END;

END LOOP;

COMMIT;

EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(SQLERRM);

END;