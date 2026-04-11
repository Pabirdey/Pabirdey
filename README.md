select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE IN('C','D','E','F');
	 
		IF V_TEMP>0 THEN		
	
      			     ------------For C Furnace
		            :BLK_CONTROL.DATE_TIME_PROD_C:=:ctl_blk.ctl_date_time_prod;
		            :BLK_CONTROL.FURNACE_C:='C';
		             SELECT ACTUAL,REPORTED,BALANCE INTO :BLK_CONTROL.ACTUAL_C,:BLK_CONTROL.REPORTED_C,:BLK_CONTROL.BALANCE_C
      		       FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			     WHERE TIMESTAMP=:ctl_blk.ctl_date_time_prod AND FURNACE='C';
      			     
      			     --#####
      			     SELECT decode(sum(ACTUAL),0,Null,sum(ACTUAL)),decode(sum(REPORTED),0,Null,sum(REPORTED)) into :BLK_CONTROL.ACTUAL_C_TD,:BLK_CONTROL.REPORTED_C_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<=:ctl_blk.ctl_date_time_prod AND FURNACE='C';
      			     --#####
