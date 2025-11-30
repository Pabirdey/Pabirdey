Select a.Timestamp,b.FUR_NAME,a.TAG_ID,b.WEB_SL_NO,b.WEB_COLUMN,Decode(b.FUR_NAME,'F',Decode(b.WEB_COLUMN,'Pellet',a.VALUE*1000,a.VALUE),a.VALUE) AS VAL_KGS,
Decode(b.FUR_NAME,'F',Decode(b.WEB_COLUMN,'Pellet',a.VALUE,a.VALUE/1000),a.VALUE/1000) AS VAL_TONS
From t_furnaces_proc_hm_prod a,T_ATOF_BIN_DETAILS b 
Where b.TAG_ID=a.TAG_ID(+) AND b.REQUIRED='Y' AND a.Timestamp='30-NOV-2025' AND b.WEB_COLUMN IS NOT NULL
Order by a.TAG_ID,b.WEB_SL_NO
