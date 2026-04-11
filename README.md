
							select sum(NET_WT) into :BLK_CONTROL.ACTUAL_C  from  demo.t_ladle_details where
 						   LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME_PROD_C+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME_PROD_C+1+6/24 
							and DESTINATION<>'R' and fur_name='C';
								
								 --#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<:ctl_blk.ctl_date_time_prod AND FURNACE='C';
      			     :BLK_CONTROL.ACTUAL_C_TD:=nvl(vActual_TD,0)+ nvl(:BLK_CONTROL.ACTUAL_C ,0);
      			     :BLK_CONTROL.REPORTED_C_TD:=nvl(vReported_TD,0)+ nvl(:BLK_CONTROL.REPORTED_C ,0);
