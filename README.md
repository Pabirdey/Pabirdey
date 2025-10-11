Select trunc(date_time,'month') DATE_MONTH,'SP1',SUM(ACTUAL_QUANTITY) NET_PROD  
FROM IMTG.t_cost_data WHERE (AREA='100000188') AND (COST_TYPE='MC') AND (COST_ELEMENT Like '%100000188%') 
AND TRUNC(DATE_TIME,'MON')>='01-SEP-2024'
Group by trunc(date_time,'month')
Union
Select Timestamp DATE_MONTH,NET_PROD From
imtg.T_SP2_PRODUCTION_MONTHLY Where Timestamp>='01-SEP-2024';
