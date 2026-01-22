PROCEDURE PROC_JODA_IOPP_PROCESS_PROC_RAW
AS
vMAXDATE DATE;
Begin
    Execute immediate 'Alter session set nls_date_format=''DD-MON-YYYY HH24:MI:SS''';
    Select MAX(DATE_TIME) into vMAXDATE From imtg.T_JODA_IOPP_PROCESS_PROC_RAW;
    IF vMAXDATE IS NULL THEN
        vMAXDATE:='01-NOV-2025';
    END IF;
    Merge INTO imtg.T_JODA_IOPP_PROCESS_PROC_RAW t
    Using (
            Select TO_DATE(SUBSTR(Date_Time,1,19),'YYYY-MM-DD HH24:MI:SS') DATE_TIME,TAG_NAME,TAG_VALUE From dbo.data_logs@IOPP_JODA s
            Where  DATE_TIME>vMAXDATE AND
            TAG_NAME IN (
            '07_WF001/TPH_PV','07_WF002/TPH_PV','07_ML01_FIC001/MV','07_ML02_FIC001/MV',
            '06_WT_001/MV','08_WT_001/MV','08_WT_002/MV','08_TK01_LIT01/MV','08_TK02_LIT01/MV',
            '13_TK01_LIT01/MV','13_TK02_LIT01/MV','13_TK03_LIT01/MV','13_TK04_LIT01/MV',
            '13_SA01_DIT001/MV','13_SA01_FIT001/MV','13_CY01_PIT01/MV','13_SA03_DIT001/MV',
            '13_SA03_FIT001/MV','13_CY02_PIT01/MV','13_WT_001/MV','13_CV01/CURR','26_TH01_ZT02/MV',
            '26_TH01_WT01/MV','26_TH01_LIT01/MV','26_TH01_AT01/MV','26_PP17_FT01/MV','26_PP17_DT01/MV',
            '26_PP17_PIT01/MV'
            )
            ORDER BY DATE_TIME            
    )s
    ON (
        t.DATE_TIME=s.DATE_TIME,
        t.TAG_NAME=s.TAG_NAME
        )
    When Matched Then
        Update Set             
            t.TAG_NAME=s.TAG_NAME,
            t.TAG_VALUE=s.TAG_VALUE
    When Not Matched Then
    INSERT(DATE_TIME,TAG_NAME,TAG_VALUE)
    VALUES(s.DATE_TIME,s.TAG_NAME,s.TAG_VALUE);
    Commit;                   
End PROC_JODA_IOPP_PROCESS_PROC_RAW;
