select distinct(TO_CHAR(BLEND_NO)) BLEND_NO, TO_CHAR(BLEND_NO) BLEND_NO from T_PSW_DAILY where SOURCE='RMBB_KNR' and BLEND_NO is not null order by 1;
