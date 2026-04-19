	select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE IN('C','D','E','F');
	 
		IF V_TEMP>0 THEN		
	
      			     ------------For C Furnace
		            :BLK_CONTROL.DATE_TIME_PROD_C:=:ctl_blk.ctl_date_time_prod;
		            :BLK_CONTROL.FURNACE_C:='C';
		             SELECT ACTUAL,REPORTED,BALANCE INTO :BLK_CONTROL.ACTUAL_C,:BLK_CONTROL.REPORTED_C,:BLK_CONTROL.BALANCE_C
      		       FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			     WHERE TIMESTAMP=:ctl_blk.ctl_date_time_prod AND FURNACE='C';
      			     
      			     
      			     SELECT decode(sum(ACTUAL),0,Null,sum(ACTUAL)),decode(sum(REPORTED),0,Null,sum(REPORTED)) into :BLK_CONTROL.ACTUAL_C_TD,:BLK_CONTROL.REPORTED_C_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<=:ctl_blk.ctl_date_time_prod AND FURNACE='C';
      			     
      			    
      			     
      			     ------------For E Furnace
		            :BLK_CONTROL.DATE_TIME_PROD_E:=:ctl_blk.ctl_date_time_prod;
		            :BLK_CONTROL.FURNACE_E:='E';
		             SELECT ACTUAL,REPORTED,BALANCE INTO :BLK_CONTROL.ACTUAL_E,:BLK_CONTROL.REPORTED_E,:BLK_CONTROL.BALANCE_E
      		       FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			     WHERE TIMESTAMP=:ctl_blk.ctl_date_time_prod AND FURNACE='E';
      			     
      			     --#####
      			     SELECT decode(sum(ACTUAL),0,Null,sum(ACTUAL)),decode(sum(REPORTED),0,Null,sum(REPORTED)) into :BLK_CONTROL.ACTUAL_E_TD,:BLK_CONTROL.REPORTED_E_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<=:ctl_blk.ctl_date_time_prod AND FURNACE='E';
      			     --#####
      			     
      			     ------------For F Furnace
		            :BLK_CONTROL.DATE_TIME_PROD_F:=:ctl_blk.ctl_date_time_prod;
		            :BLK_CONTROL.FURNACE_F:='F';
		             SELECT ACTUAL,REPORTED,BALANCE INTO :BLK_CONTROL.ACTUAL_F,:BLK_CONTROL.REPORTED_F,:BLK_CONTROL.BALANCE_F
      		       FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			     WHERE TIMESTAMP=:ctl_blk.ctl_date_time_prod AND FURNACE='F';
      			     
      			     --#####
      			     SELECT decode(sum(ACTUAL),0,Null,sum(ACTUAL)),decode(sum(REPORTED),0,Null,sum(REPORTED)) into :BLK_CONTROL.ACTUAL_F_TD,:BLK_CONTROL.REPORTED_F_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<=:ctl_blk.ctl_date_time_prod AND FURNACE='F';
      			     --#####
      			     
      			     ---- For A-F Actual
      			   
                   :BLK_CONTROL.DISPLAY_ACTUAL:=nvl(:BLK_CONTROL.ACTUAL_C,0)+nvl(:BLK_CONTROL.ACTUAL_D,0)+nvl(:BLK_CONTROL.ACTUAL_E,0)+nvl(:BLK_CONTROL.ACTUAL_F,0);
                 ---- For A-F Reported
      			   
      			     :BLK_CONTROL.DISPLAY_REPORTED:=nvl(:BLK_CONTROL.REPORTED_C,0)+nvl(:BLK_CONTROL.REPORTED_D,0)+nvl(:BLK_CONTROL.REPORTED_E,0)+nvl(:BLK_CONTROL.REPORTED_F,0);
      			     
      			     ---- For A-F Balance
      			   
      			     :BLK_CONTROL.DISPLAY_BALANCE:=nvl(:BLK_CONTROL.BALANCE_C,0)+nvl(:BLK_CONTROL.BALANCE_D,0)+nvl(:BLK_CONTROL.BALANCE_E,0)+nvl(:BLK_CONTROL.BALANCE_F,0);
      			     --##### For A-F Actual Todate/Reported
							
				
			    
			    SELECT SUM(NVL(ACTUAL,0)-NVL(REPORTED,0))INTO :BLK_CONTROL.BALANCE_C FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE 
					TIMESTAMP>=TRUNC(:BLK_CONTROL.DATE_TIME_PROD_C,'MON') AND TIMESTAMP<:BLK_CONTROL.DATE_TIME_PROD_C AND FURNACE=:BLK_CONTROL.FURNACE_C;
			    
