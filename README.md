Declare
	v_temp         NUMBER;
	V_TEMP1        NUMBER;
	v_total_rows   number;
	V_Row_Count    number;
	v_group_id		 number(6);
	VBAL    NUMBER;
	vday number;
	vbal_A number;
	vbal_B number;
	vbal_C number;
	vbal_D number;
	vbal_E number;
	vbal_F number;
	vActual_TD Number;
	vReported_TD Number;
	vLD1_TONS_ACTUAL_TD Number;
	vLD2_TONS_ACTUAL_TD Number;
	vLD3_TONS_ACTUAL_TD Number;
	vMRD_TONS_ACTUAL_TD Number;
	vNO_TP_TD Number;
Begin
  set_item_property('BLK_CONTROL.PB_OK_TEMP',VISIBLE,PROPERTY_FALSE);
	:Global.vBalance:=0;
	:Global.vBalance_H:=0;
	:Global.vBalance_I:=0;
	:Global.slag:=0;
 
 
    set_item_property('BLK_CONTROL.DISP_ACTUAL',VISIBLE,PROPERTY_TRUE);
		Begin
				 
				 set_item_property('CTL_BLK.TXT_RPT_G',INSERT_ALLOWED,PROPERTY_FALSE);
				 set_item_property('CTL_BLK.TXT_RPT_G',update_ALLOWED,PROPERTY_FALSE);
				 
				 set_item_property('CTL_BLK.TXT_RPT_H',INSERT_ALLOWED,PROPERTY_FALSE);
				 set_item_property('CTL_BLK.TXT_RPT_H',update_ALLOWED,PROPERTY_FALSE);
				 
				 set_item_property('CTL_BLK.TXT_RPT_I',INSERT_ALLOWED,PROPERTY_FALSE);
				 set_item_property('CTL_BLK.TXT_RPT_I',update_ALLOWED,PROPERTY_FALSE);
				 
				 
				        set_item_property('BLK_CONTROL.reported_C',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_C',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',update_ALLOWED,PROPERTY_FALSE);
		            
		            set_item_property('BLK_CONTROL.SLAG_LADLE',UPDATE_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.SLAG_LADLE',INSERT_ALLOWED,PROPERTY_FALSE);
		            
		      ----- END      	
				 
				 IF :global.username='BFCTRL' THEN
				 	      ----- Change in 30-jul-2007
				 	      set_item_property('BLK_CONTROL.reported_C',INSERT_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_C',update_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_D',INSERT_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_D',update_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_E',INSERT_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_E',update_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_F',INSERT_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.reported_F',update_ALLOWED,PROPERTY_TRUE);
		            
		            set_item_property('BLK_CONTROL.SLAG_LADLE',UPDATE_ALLOWED,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.SLAG_LADLE',INSERT_ALLOWED,PROPERTY_TRUE);
		       
				 
				 		set_item_property('CTL_BLK.TXT_RPT_G',INSERT_ALLOWED,PROPERTY_FALSE);
				 		set_item_property('CTL_BLK.TXT_RPT_G',update_ALLOWED,PROPERTY_FALSE);	
				 		
				 		set_item_property('CTL_BLK.TXT_RPT_H',INSERT_ALLOWED,PROPERTY_FALSE);
				 		set_item_property('CTL_BLK.TXT_RPT_H',update_ALLOWED,PROPERTY_FALSE);	
				 		
				 		set_item_property('CTL_BLK.TXT_RPT_I',INSERT_ALLOWED,PROPERTY_FALSE);
				 		set_item_property('CTL_BLK.TXT_RPT_I',update_ALLOWED,PROPERTY_FALSE);	
				 		:BLK_CONTROL.DISP_ACTUAL:='ACTUAL BREAKUP';
				 	
				 		set_item_property('BLK_CONTROL.DATE_TIME_H',VISIBLE,PROPERTY_FALSE);
				 		set_item_property('BLK_CONTROL.LD1_TONS_ACTUAL',VISIBLE,PROPERTY_TRUE);
						set_item_property('BLK_CONTROL.LD2_TONS_ACTUAL',VISIBLE,PROPERTY_TRUE);
						set_item_property('BLK_CONTROL.LD3_TONS_ACTUAL',VISIBLE,PROPERTY_TRUE);
						set_item_property('BLK_CONTROL.MRDTP_TONS_ACTUAL',VISIBLE,PROPERTY_TRUE);
				 			 					 	
				 ELSIF :global.username='GBFCTRL'  THEN
				 			set_item_property('CTL_BLK.TXT_RPT_G',INSERT_ALLOWED,PROPERTY_TRUE);
				 			set_item_property('CTL_BLK.TXT_RPT_G',update_ALLOWED,PROPERTY_TRUE);
				 			
				 			set_item_property('CTL_BLK.TXT_RPT_H',INSERT_ALLOWED,PROPERTY_FALSE);
				 			set_item_property('CTL_BLK.TXT_RPT_H',update_ALLOWED,PROPERTY_FALSE);
				 			
				 			set_item_property('CTL_BLK.TXT_RPT_I',INSERT_ALLOWED,PROPERTY_FALSE);
				 			set_item_property('CTL_BLK.TXT_RPT_I',update_ALLOWED,PROPERTY_FALSE);
				 			
				 			---- CHANGE IN 30-JUL-2007 
				        set_item_property('BLK_CONTROL.reported_C',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_C',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.DISP_ACTUAL',VISIBLE,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.SLAG_LADLE',VISUAL_ATTRIBUTE,'VIS_DEFAULT');
		            :BLK_CONTROL.DISP_ACTUAL:='ACTUAL BREAKUP';
		           	set_item_property('BLK_CONTROL.DATE_TIME_H',VISIBLE,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.LD1_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD2_TONS',VISIBLE,PROPERTY_FALSE);
									set_item_property('BLK_CONTROL.LD3_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.MRDTP_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD1_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.LD2_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.LD3_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.MRDTP_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
				 		
				 		ELSIF :global.username='HBFCTRL'  THEN
				 				   
				 				   	set_item_property('CTL_BLK.TXT_RPT_G',INSERT_ALLOWED,PROPERTY_FALSE);
				 						set_item_property('CTL_BLK.TXT_RPT_G',update_ALLOWED,PROPERTY_FALSE);
				 									 						
				 						set_item_property('CTL_BLK.TXT_RPT_H',INSERT_ALLOWED,PROPERTY_TRUE);
				 						set_item_property('CTL_BLK.TXT_RPT_H',update_ALLOWED,PROPERTY_TRUE);
				 						
				 						----CHANGE IN 25-MAR-2012
				 						set_item_property('CTL_BLK.TXT_RPT_I',INSERT_ALLOWED,PROPERTY_FALSE);
				 						set_item_property('CTL_BLK.TXT_RPT_I',update_ALLOWED,PROPERTY_FALSE);
				 			
				 						---- CHANGE IN 30-JUL-2007 
				        		set_item_property('BLK_CONTROL.reported_C',INSERT_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_C',update_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_D',INSERT_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_D',update_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_E',INSERT_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_E',update_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_F',INSERT_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.reported_F',update_ALLOWED,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.DISP_ACTUAL',VISIBLE,PROPERTY_TRUE);
		            		set_item_property('BLK_CONTROL.SLAG_LADLE',VISUAL_ATTRIBUTE,'VIS_DEFAULT');
		            		:BLK_CONTROL.DISP_ACTUAL:='ACTUAL BREAKUP';
		            		set_item_property('BLK_CONTROL.DATE_TIME_H',VISIBLE,PROPERTY_FALSE);
		            		set_item_property('BLK_CONTROL.LD1_TONS',VISIBLE,PROPERTY_FALSE);
										set_item_property('BLK_CONTROL.LD2_TONS',VISIBLE,PROPERTY_FALSE);
											set_item_property('BLK_CONTROL.LD3_TONS',VISIBLE,PROPERTY_FALSE);
										set_item_property('BLK_CONTROL.MRDTP_TONS',VISIBLE,PROPERTY_FALSE);		
										set_item_property('BLK_CONTROL.LD1_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD2_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD3_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.MRDTP_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
								
								ELSIF :global.username='IBFCTRL'  THEN
				 			set_item_property('CTL_BLK.TXT_RPT_G',INSERT_ALLOWED,PROPERTY_FALSE);
				 			set_item_property('CTL_BLK.TXT_RPT_G',update_ALLOWED,PROPERTY_FALSE);
				 			
				 			set_item_property('CTL_BLK.TXT_RPT_H',INSERT_ALLOWED,PROPERTY_FALSE);
				 			set_item_property('CTL_BLK.TXT_RPT_H',update_ALLOWED,PROPERTY_FALSE);
				 			
				 			set_item_property('CTL_BLK.TXT_RPT_I',INSERT_ALLOWED,PROPERTY_TRUE);
				 			set_item_property('CTL_BLK.TXT_RPT_I',update_ALLOWED,PROPERTY_TRUE);
				 			
				 			---- CHANGE IN 30-JUL-2007 
				        set_item_property('BLK_CONTROL.reported_C',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_C',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_D',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_E',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',INSERT_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.reported_F',update_ALLOWED,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.DISP_ACTUAL',VISIBLE,PROPERTY_TRUE);
		            set_item_property('BLK_CONTROL.SLAG_LADLE',VISUAL_ATTRIBUTE,'VIS_DEFAULT');
		            :BLK_CONTROL.DISP_ACTUAL:='ACTUAL BREAKUP';
		           	set_item_property('BLK_CONTROL.DATE_TIME_H',VISIBLE,PROPERTY_FALSE);
		            set_item_property('BLK_CONTROL.LD1_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD2_TONS',VISIBLE,PROPERTY_FALSE);
									set_item_property('BLK_CONTROL.LD3_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.MRDTP_TONS',VISIBLE,PROPERTY_FALSE);
								set_item_property('BLK_CONTROL.LD1_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.LD2_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.LD3_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
							set_item_property('BLK_CONTROL.MRDTP_TONS_ACTUAL',VISIBLE,PROPERTY_FALSE);
				 		            		
		         END IF; 		
		           
		      
		End;
     
                                                                                                                                                                                                                                                                                  
    --Go_Block('T_BF_PRODUCTION');
    Go_Block('BLK_CONTROL');
    CLEAR_BLOCK(no_commit);
    
                   
       							SELECT AVG(SLAG_GRANULATION)/(10.5*1.15) INTO :BLK_CONTROL.SLAG_LADLE FROM DEMO.T_BF_PRODUCTION_TEST 
      			        WHERE TIMESTAMP=:CTL_BLK.CTL_DATE_TIME_PROD AND FUR_NO in ('C','D','E','F');		     
		  

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
      			   
      			     :BLK_CONTROL.DISPLAY_ACTUAL_TD:=nvl(:BLK_CONTROL.ACTUAL_C_TD,0)+nvl(:BLK_CONTROL.ACTUAL_D_TD,0)+nvl(:BLK_CONTROL.ACTUAL_E_TD,0)+nvl(:BLK_CONTROL.ACTUAL_F_TD,0);
      			     :BLK_CONTROL.DISPLAY_REPORTED_TD:=nvl(:BLK_CONTROL.REPORTED_C_TD,0)+nvl(:BLK_CONTROL.REPORTED_D_TD,0)+nvl(:BLK_CONTROL.REPORTED_E_TD,0)+nvl(:BLK_CONTROL.REPORTED_F_TD,0);
      			     --#####
	
       							--Modified on 15-Jan-2009
                    select DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME,:BLK_CONTROL.LD1_TONS,:BLK_CONTROL.LD2_TONS,:BLK_CONTROL.LD3_TONS,:BLK_CONTROL.MRDTP_TONS,:BLK_CONTROL.NOOFTP,
		                     :BLK_CONTROL.LD1_TONS_ACTUAL,:BLK_CONTROL.LD2_TONS_ACTUAL,:BLK_CONTROL.LD3_TONS_ACTUAL,:BLK_CONTROL.MRDTP_TONS_ACTUAL		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='A-F';
		                -------------------
		                ---------------------------  End   --------------------------------------------
		
   
		ELSE
					 
					
				:BLK_CONTROL.DATE_TIME_PROD_C:=:ctl_blk.ctl_date_time_prod;
		    :BLK_CONTROL.FURNACE_C:='C';	

				  
							
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
      			     If :BLK_CONTROL.ACTUAL_C_TD=0 Then
      			     	  :BLK_CONTROL.ACTUAL_C_TD:=Null;
      			     End If; 
      			     If :BLK_CONTROL.REPORTED_C_TD=0 Then
      			     	  :BLK_CONTROL.REPORTED_C_TD:=Null;
      			     End If;        			     
      			     --#####
							
				
			    
			    SELECT SUM(NVL(ACTUAL,0)-NVL(REPORTED,0))INTO :BLK_CONTROL.BALANCE_C FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE 
					TIMESTAMP>=TRUNC(:BLK_CONTROL.DATE_TIME_PROD_C,'MON') AND TIMESTAMP<:BLK_CONTROL.DATE_TIME_PROD_C AND FURNACE=:BLK_CONTROL.FURNACE_C;
			    
					
					:BLK_CONTROL.DATE_TIME_PROD_E:=:ctl_blk.ctl_date_time_prod;
		      :BLK_CONTROL.FURNACE_E:='E';
					
			
							
						select sum(NET_WT) into :BLK_CONTROL.ACTUAL_E  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME_PROD_E+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME_PROD_E+1+6/24 
							and DESTINATION<>'R' and fur_name='E';	
								--#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<:ctl_blk.ctl_date_time_prod AND FURNACE='E';
      			     :BLK_CONTROL.ACTUAL_E_TD:=nvl(vActual_TD,0)+ nvl(:BLK_CONTROL.ACTUAL_E ,0);
      			     :BLK_CONTROL.REPORTED_E_TD:=nvl(vReported_TD,0)+ nvl(:BLK_CONTROL.REPORTED_E ,0);  
      			     If :BLK_CONTROL.ACTUAL_E_TD=0 Then
      			     	  :BLK_CONTROL.ACTUAL_E_TD:=Null;
      			     End If; 
      			     If :BLK_CONTROL.REPORTED_E_TD=0 Then
      			     	  :BLK_CONTROL.REPORTED_E_TD:=Null;
      			     End If;      			     
      			     --#####
							
			    
						
						SELECT SUM(NVL(ACTUAL,0)-NVL(REPORTED,0))INTO :BLK_CONTROL.BALANCE_E FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE 
						TIMESTAMP>=TRUNC(:BLK_CONTROL.DATE_TIME_PROD_E,'MON') AND TIMESTAMP<:BLK_CONTROL.DATE_TIME_PROD_E AND FURNACE=:BLK_CONTROL.FURNACE_E; 
						   
			
		
					
					:BLK_CONTROL.DATE_TIME_PROD_F:=:ctl_blk.ctl_date_time_prod;
		      :BLK_CONTROL.FURNACE_F:='F';

				 
							
							select sum(NET_WT) into :BLK_CONTROL.ACTUAL_F  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME_PROD_F+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME_PROD_F+1+6/24 
							and DESTINATION<>'R' and fur_name='F';
								 
								 --#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:ctl_blk.ctl_date_time_prod,'MON') AND TIMESTAMP<:ctl_blk.ctl_date_time_prod AND FURNACE='F';
      			     :BLK_CONTROL.ACTUAL_F_TD:=nvl(vActual_TD,0)+ nvl(:BLK_CONTROL.ACTUAL_F ,0);
      			     :BLK_CONTROL.REPORTED_F_TD:=nvl(vReported_TD,0)+ nvl(:BLK_CONTROL.REPORTED_F ,0);   
      			     If :BLK_CONTROL.ACTUAL_F_TD=0 Then
      			     	  :BLK_CONTROL.ACTUAL_F_TD:=Null;
      			     End If; 
      			     If :BLK_CONTROL.REPORTED_F_TD=0 Then
      			     	  :BLK_CONTROL.REPORTED_F_TD:=Null;
      			     End If;   			     
      			     --#####
							
												
			
					
			   	SELECT SUM(NVL(ACTUAL,0)-NVL(REPORTED,0))INTO :BLK_CONTROL.BALANCE_F FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE 
					TIMESTAMP>=TRUNC(:BLK_CONTROL.DATE_TIME_PROD_F,'MON') AND TIMESTAMP<:BLK_CONTROL.DATE_TIME_PROD_F AND FURNACE=:BLK_CONTROL.FURNACE_F;
					
	

		
			 --- FOR T_LADLE
			:BLK_CONTROL.DATE_TIME:=:ctl_blk.ctl_date_time_prod;
				
			-- LD1 Tonnage
			
			
					
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24					
					 AND DESTINATION='LD1' and fur_name IN ('C','D','E','F');	
					:BLK_CONTROL.LD1_TONS_ACTUAL:=:BLK_CONTROL.LD1_TONS;
					
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24			
						AND DESTINATION='LD2' and fur_name IN ('C','D','E','F');	
					:BLK_CONTROL.LD2_TONS_ACTUAL:=:BLK_CONTROL.LD2_TONS;					
			
						
			SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						-- AND DESTINATION='LD2' and fur_name<>'G';
						AND DESTINATION='LD3' and fur_name IN ('C','D','E','F');	
					:BLK_CONTROL.LD3_TONS_ACTUAL:=:BLK_CONTROL.LD3_TONS;
			
						SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.MRDTP_TONS from  demo.t_ladle_details where
		 			  LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					--	AND DESTINATION='MRD' AND TRP_NO<=50 and fur_name<>'G';		
					AND DESTINATION='MRD' AND TRP_NO<=50 and fur_name IN ('C','D','E','F');			
				  	:BLK_CONTROL.MRDTP_TONS_ACTUAL:=:BLK_CONTROL.MRDTP_TONS;
									
		     	SELECT NVL(SUM(FILL_STATUS),0) INTO :BLK_CONTROL.NOOFTP from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					--	AND  TRP_NO<=50 and fur_name<>'G' and ret_flag='N';
							AND  TRP_NO<=50 and fur_name IN ('C','D','E','F') and ret_flag='N';
						

					  ---- For A-F Actual      			     
                 :BLK_CONTROL.DISPLAY_ACTUAL:=nvl(:BLK_CONTROL.ACTUAL_C,0)+nvl(:BLK_CONTROL.ACTUAL_D,0)+nvl(:BLK_CONTROL.ACTUAL_E,0)+nvl(:BLK_CONTROL.ACTUAL_F,0);
                                 
                 ---- For A-F Reported      			     
      			     :BLK_CONTROL.DISPLAY_REPORTED:=nvl(:BLK_CONTROL.REPORTED_C,0)+nvl(:BLK_CONTROL.REPORTED_D,0)+nvl(:BLK_CONTROL.REPORTED_E,0)+nvl(:BLK_CONTROL.REPORTED_F,0);
      			     
      			     	---- For A-F Balance      			     
      			     :BLK_CONTROL.DISPLAY_BALANCE:=nvl(:BLK_CONTROL.BALANCE_C,0)+nvl(:BLK_CONTROL.BALANCE_D,0)+nvl(:BLK_CONTROL.BALANCE_E,0)+nvl(:BLK_CONTROL.BALANCE_F,0);
      			  
      			     --##### For A-F Actual Todate/Reported      			     
      			     :BLK_CONTROL.DISPLAY_ACTUAL_TD:=nvl(:BLK_CONTROL.ACTUAL_C_TD,0)+nvl(:BLK_CONTROL.ACTUAL_D_TD,0)+nvl(:BLK_CONTROL.ACTUAL_E_TD,0)+nvl(:BLK_CONTROL.ACTUAL_F_TD,0);
      			     :BLK_CONTROL.DISPLAY_REPORTED_TD:=nvl(:BLK_CONTROL.REPORTED_C_TD,0)+nvl(:BLK_CONTROL.REPORTED_D_TD,0)+nvl(:BLK_CONTROL.REPORTED_E_TD,0)+nvl(:BLK_CONTROL.REPORTED_F_TD,0);
      			     
      			    vday:=to_char(to_date(:ctl_blk.ctl_date_time_prod),'DD');
		     if vday=1 then	
		     	  
		     	
		     	             GO_ITEM('BLK_CONTROL.REPORTED_C');		     	          
		     	             IF :BLK_CONTROL.ACTUAL_C IS NOT NULL THEN		     	                
		     	                    :BLK_CONTROL.REPORTED_C:=NVL(:BLK_CONTROL.ACTUAL_C,0)+0;
		     	             end if;
		     	             
		     	  --for D Fur
		     	             GO_ITEM('BLK_CONTROL.REPORTED_D');		     	             
		     	             IF :BLK_CONTROL.ACTUAL_D IS NOT NULL THEN		     	                   
		     	                      :BLK_CONTROL.REPORTED_D:=NVL(:BLK_CONTROL.ACTUAL_D,0)+0;
		     	             end if;
		     	             
		     	 --for E Fur
		     	             GO_ITEM('BLK_CONTROL.REPORTED_E');	     	             
		     	             IF :BLK_CONTROL.ACTUAL_E IS NOT NULL THEN		     	                
		     	                   :BLK_CONTROL.REPORTED_E:=NVL(:BLK_CONTROL.ACTUAL_E,0)+0;
		     	             end if;
		     	             
		     	--for F Fur
		     	             GO_ITEM('BLK_CONTROL.REPORTED_F');		     	            
		     	             IF :BLK_CONTROL.ACTUAL_F IS NOT NULL THEN		     	                   
		     	                      :BLK_CONTROL.REPORTED_F:=NVL(:BLK_CONTROL.ACTUAL_F,0)+0;
		     	             end if;
		     	             GO_ITEM('BLK_CONTROL.REPORTED_C');
		     	            	
				
				 else
				  
					
					IF :BLK_CONTROL.ACTUAL_C IS NOT NULL THEN
						:BLK_CONTROL.REPORTED_C:=NVL(:BLK_CONTROL.ACTUAL_C,0)+NVL(:BLK_CONTROL.BALANCE_C,0); 
					END IF;
					GO_ITEM('BLK_CONTROL.REPORTED_D');
					
       
					IF :BLK_CONTROL.ACTUAL_D IS NOT NULL THEN
						:BLK_CONTROL.REPORTED_D:=NVL(:BLK_CONTROL.ACTUAL_D,0)+NVL(:BLK_CONTROL.BALANCE_D,0); 
					END IF;
					GO_ITEM('BLK_CONTROL.REPORTED_E');
					
				
					
					IF :BLK_CONTROL.ACTUAL_E IS NOT NULL THEN
						:BLK_CONTROL.REPORTED_E:=NVL(:BLK_CONTROL.ACTUAL_E,0)+NVL(:BLK_CONTROL.BALANCE_E,0); 
					END IF;
					
					GO_ITEM('BLK_CONTROL.REPORTED_F');
					
			
					
					IF :BLK_CONTROL.ACTUAL_F IS NOT NULL THEN
						:BLK_CONTROL.REPORTED_F:=NVL(:BLK_CONTROL.ACTUAL_F,0)+NVL(:BLK_CONTROL.BALANCE_F,0); 
					END IF;
					GO_ITEM('BLK_CONTROL.REPORTED_C');
			end if;		
			
			END IF;
			

		V_TEMP:=0;	
		select COUNT(*) INTO V_TEMP from DEMO.T_LADLE where DATE_TIME=:ctl_blk.ctl_date_time_prod and PLANT ='G'; 
		
		IF V_TEMP>0 THEN 	
			
					
 				select DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME,:BLK_CONTROL.LD1_TONS_G,:BLK_CONTROL.LD2_TONS_G,:BLK_CONTROL.LD3_TONS_G,:BLK_CONTROL.MRDTP_TONS_G,:BLK_CONTROL.NOOFTP_G,
		                     :BLK_CONTROL.LD1_TONS_ACTUAL_G,:BLK_CONTROL.LD2_TONS_ACTUAL_G,:BLK_CONTROL.LD3_TONS_ACTUAL_G,:BLK_CONTROL.MRDTP_TONS_ACTUAL_G		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='G';

		                
		Else

				SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					 AND DESTINATION='LD1' and fur_name='G';	
					:BLK_CONTROL.LD1_TONS_ACTUAL_G:=:BLK_CONTROL.LD1_TONS_G;
					
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD2' and fur_name ='G';	
					:BLK_CONTROL.LD2_TONS_ACTUAL_G:=:BLK_CONTROL.LD2_TONS_G;
						
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD3' and fur_name ='G';	
					:BLK_CONTROL.LD3_TONS_ACTUAL_G:=:BLK_CONTROL.LD3_TONS_G;
					
						SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.MRDTP_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='MRD' and fur_name ='G';	
				:BLK_CONTROL.MRDTP_TONS_ACTUAL_G:=:BLK_CONTROL.MRDTP_TONS_G;
				
				SELECT NVL(SUM(FILL_STATUS),0) INTO :BLK_CONTROL.NOOFTP_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
							AND  TRP_NO<=50 and fur_name ='G' and ret_flag='N';
							
		End If;
		

		
		V_TEMP:=0;
		select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE ='G';    
 		
 		:CTL_BLK.TXT_TIMESTAMP_G:=:ctl_blk.ctl_date_time_prod;
			:CTL_BLK.TXT_FURNACE_G:='G';
			:CTL_BLK.TXT_ACTUAL_G:=NULL;
			:CTL_BLK.TXT_RPT_G:=NULL;
			:CTL_BLK.TXT_BAL_G:=NULL;
			:CTL_BLK.DISPLAY_ACT_G:=NULL;
			:CTL_BLK.DISPLAY_RPT_G:=NULL;
			:CTL_BLK.DISPLAY_BAL_G:=NULL;

 			IF V_TEMP>0 THEN 			

 				SELECT ACTUAL,REPORTED,BALANCE INTO :CTL_BLK.TXT_ACTUAL_G ,:CTL_BLK.TXT_RPT_G,:CTL_BLK.TXT_BAL_G
      		FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      
      					 --#####
      			     SELECT sum(ACTUAL),sum(REPORTED) into :CTL_BLK.TXT_ACTUAL_G_TD ,:CTL_BLK.TXT_RPT_G_TD
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<=:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      			     --#####	
       	SELECT BALANCE INTO :Global.vBalance FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=(:CTL_BLK.TXT_TIMESTAMP_G)-1 AND FURNACE='G';	 
 			ELSE					

				Select SUM(NET_WT) into :CTL_BLK.TXT_ACTUAL_G  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:CTL_BLK.TXT_TIMESTAMP_G+6/24 and LADLE_FLEND_TIME<:CTL_BLK.TXT_TIMESTAMP_G+1+6/24 
							and DESTINATION<>'R' and fur_name='G';
			
				SELECT SUM(NVL(ACTUAL,0))-sum(NVL(REPORTED,0)) INTO :CTL_BLK.TXT_BAL_G
					FROM DEMO.T_BF_PRODUCTION_TRACKING 
						WHERE TIMESTAMP>=TRUNC(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G'; 			
			
		  	:CTL_BLK.TXT_RPT_G:=nvl(:CTL_BLK.TXT_ACTUAL_G,0)+nvl(:CTL_BLK.TXT_BAL_G,0);	
		  	:Global.vBalance:=:CTL_BLK.TXT_BAL_G;
				:CTL_BLK.TXT_BAL_G:=NVL(:CTL_BLK.TXT_ACTUAL_G,0)-NVL(:CTL_BLK.TXT_RPT_G,0)+NVL(:Global.vBalance,0);	
				
			         	--#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      			     :CTL_BLK.TXT_ACTUAL_G_TD:=nvl(vActual_TD,0)+ nvl(:CTL_BLK.TXT_ACTUAL_G ,0);
      			     	:CTL_BLK.TXT_RPT_G_TD:=nvl(vReported_TD,0)+ nvl(:CTL_BLK.TXT_RPT_G ,0);      			     
      			     --#####	   		  			
 			END IF;
 	
		:CTL_BLK.DISPLAY_ACT_G:=nvl(:BLK_CONTROL.DISPLAY_ACTUAL,0)+nvl(:CTL_BLK.TXT_ACTUAL_G,0);
		:CTL_BLK.DISPLAY_RPT_G:=nvl(:BLK_CONTROL.DISPLAY_REPORTED,0)+nvl(:CTL_BLK.TXT_RPT_G,0);
		:CTL_BLK.DISPLAY_BAL_G:=nvl(:BLK_CONTROL.DISPLAY_BALANCE,0)+nvl(:CTL_BLK.TXT_BAL_G,0);
							
		--#####
		:CTL_BLK.DISPLAY_ACT_G_TD:=nvl(:BLK_CONTROL.DISPLAY_ACTUAL_TD,0)+nvl(:CTL_BLK.TXT_ACTUAL_G_TD,0);
		:CTL_BLK.DISPLAY_RPT_G_TD:=nvl(:BLK_CONTROL.DISPLAY_REPORTED_TD,0)+nvl(:CTL_BLK.TXT_RPT_G_TD,0);     			    
		--#####
		
									If :CTL_BLK.TXT_ACTUAL_G_TD=0 Then
      			     		:CTL_BLK.TXT_ACTUAL_G_TD:=Null;
      			     	End If;   
      			     	If :CTL_BLK.TXT_RPT_G_TD=0 Then
      			     		 :CTL_BLK.TXT_RPT_G_TD:=Null;
      			     	End If; 
		
		----------------------- For H Blast Furnace 
		 V_TEMP:=0;
		 select COUNT(*) INTO V_TEMP from DEMO.T_LADLE where DATE_TIME=:ctl_blk.ctl_date_time_prod and PLANT ='H';    
		 IF V_TEMP>0 THEN 				
 				select DATE_TIME,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME, :BLK_CONTROL.LD1_TONS_ACTUAL_H,:BLK_CONTROL.LD2_TONS_ACTUAL_H,:BLK_CONTROL.LD3_TONS_ACTUAL_H,:BLK_CONTROL.MRDTP_TONS_ACTUAL_H		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='H';
		 Else
		 		SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS_ACTUAL_H from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					 AND DESTINATION='LD1' and fur_name='H';

				SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS_ACTUAL_H from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD2' and fur_name ='H';

        SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS_ACTUAL_H from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD3' and fur_name ='H';
						
				SELECT NVL(SUM(NET_WT),0) INTO 	:BLK_CONTROL.MRDTP_TONS_ACTUAL_H from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='MRD' and fur_name ='H';
		 End If;
		 
		 
		 
		 
		 V_TEMP:=0;
		 select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE ='H'; 
		 
 			:CTL_BLK.TXT_TIMESTAMP_H:=:ctl_blk.ctl_date_time_prod;
			:CTL_BLK.TXT_FURNACE_H:='H';
			:CTL_BLK.TXT_ACTUAL_H:=NULL;
			:CTL_BLK.TXT_RPT_H:=NULL;
			:CTL_BLK.TXT_BAL_H:=NULL;
			:CTL_BLK.DISPLAY_ACT_H:=NULL;
			:CTL_BLK.DISPLAY_RPT_H:=NULL;
			:CTL_BLK.DISPLAY_BAL_H:=NULL;

 			IF V_TEMP>0 THEN
 				 			 		
 				SELECT ACTUAL,REPORTED,BALANCE INTO :CTL_BLK.TXT_ACTUAL_H ,:CTL_BLK.TXT_RPT_H,:CTL_BLK.TXT_BAL_H
      		FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=:CTL_BLK.TXT_TIMESTAMP_H AND FURNACE='H'; 
      					 --#####
      			     SELECT sum(ACTUAL),sum(REPORTED) into :CTL_BLK.TXT_ACTUAL_H_TD ,:CTL_BLK.TXT_RPT_H_TD
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_H,'MON') AND TIMESTAMP<=:CTL_BLK.TXT_TIMESTAMP_H AND FURNACE='H';
      			     --#####
       SELECT BALANCE INTO :Global.vBalance_H FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=(:CTL_BLK.TXT_TIMESTAMP_G)-1 AND FURNACE='H';	
 			ELSE
 				
				Select SUM(NET_WT) into :CTL_BLK.TXT_ACTUAL_H  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:CTL_BLK.TXT_TIMESTAMP_H+6/24 and LADLE_FLEND_TIME<:CTL_BLK.TXT_TIMESTAMP_H+1+6/24 
							and DESTINATION<>'R' and fur_name='H';
			
				SELECT SUM(NVL(ACTUAL,0))-sum(NVL(REPORTED,0)) INTO :CTL_BLK.TXT_BAL_H FROM 
					DEMO.T_BF_PRODUCTION_TRACKING 
						WHERE TIMESTAMP>=TRUNC(:CTL_BLK.TXT_TIMESTAMP_H,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_H AND FURNACE='H'; 			
			
		  	:CTL_BLK.TXT_RPT_H:=nvl(:CTL_BLK.TXT_ACTUAL_H,0)+nvl(:CTL_BLK.TXT_BAL_H,0);	
		  	:Global.vBalance_H:=:CTL_BLK.TXT_BAL_H;
				:CTL_BLK.TXT_BAL_H:=NVL(:CTL_BLK.TXT_ACTUAL_H,0)-NVL(:CTL_BLK.TXT_RPT_H,0)+NVL(:Global.vBalance_H,0);		 
				
								--#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_H,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_H AND FURNACE='H';
      			     :CTL_BLK.TXT_ACTUAL_H_TD:=nvl(vActual_TD,0)+ nvl(:CTL_BLK.TXT_ACTUAL_H ,0);
      			     :CTL_BLK.TXT_RPT_H_TD:=nvl(vReported_TD,0)+ nvl(:CTL_BLK.TXT_RPT_H ,0); 
      			     	 
      			     --#####	   		  			
 			END IF;
 
		:CTL_BLK.DISPLAY_ACT_H:=nvl(:CTL_BLK.DISPLAY_ACT_G,0)+nvl(:CTL_BLK.TXT_ACTUAL_H,0);
		:CTL_BLK.DISPLAY_RPT_H:=nvl(:CTL_BLK.DISPLAY_RPT_G,0)+nvl(:CTL_BLK.TXT_RPT_H,0);
		:CTL_BLK.DISPLAY_BAL_H:=nvl(:CTL_BLK.DISPLAY_BAL_G,0)+nvl(:CTL_BLK.TXT_BAL_H,0);

		--#####
		:CTL_BLK.DISPLAY_ACT_H_TD:=nvl(:CTL_BLK.DISPLAY_ACT_G_TD,0)+nvl(:CTL_BLK.TXT_ACTUAL_H_TD,0);
		:CTL_BLK.DISPLAY_RPT_H_TD:=nvl(:CTL_BLK.DISPLAY_RPT_G_TD,0)+nvl(:CTL_BLK.TXT_RPT_H_TD,0);     			    
		--#####
		
									If :CTL_BLK.TXT_ACTUAL_H_TD=0 Then
      			     		:CTL_BLK.TXT_ACTUAL_H_TD:=Null;
      			     	End If;   
      			     	If :CTL_BLK.TXT_RPT_H_TD=0 Then
      			     		 :CTL_BLK.TXT_RPT_H_TD:=Null;
      			     	End If;  
      			     	
 --------------------------------------------------------------------------------------------------------------------
 	----------------------- For I Blast Furnace 
		 V_TEMP:=0;
		 select COUNT(*) INTO V_TEMP from DEMO.T_LADLE where DATE_TIME=:ctl_blk.ctl_date_time_prod and PLANT ='I';    
		 IF V_TEMP>0 THEN 				
 				select DATE_TIME,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME, :BLK_CONTROL.LD1_TONS_ACTUAL_I,:BLK_CONTROL.LD2_TONS_ACTUAL_I,:BLK_CONTROL.LD3_TONS_ACTUAL_I,:BLK_CONTROL.MRDTP_TONS_ACTUAL_I		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='I';
		 Else
		 		SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS_ACTUAL_I from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					 AND DESTINATION='LD1' and fur_name='I';

				SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS_ACTUAL_I from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD2' and fur_name ='I';

        SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS_ACTUAL_I from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD3' and fur_name ='I';
						
				SELECT NVL(SUM(NET_WT),0) INTO 	:BLK_CONTROL.MRDTP_TONS_ACTUAL_I from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='MRD' and fur_name ='I';
		 End If;
		 
		 
		 
		 
		 V_TEMP:=0;
		 select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE ='I'; 
		 
 			:CTL_BLK.TXT_TIMESTAMP_I:=:ctl_blk.ctl_date_time_prod;
			:CTL_BLK.TXT_FURNACE_I:='I';
			:CTL_BLK.TXT_ACTUAL_I:=NULL;
			:CTL_BLK.TXT_RPT_I:=NULL;
			:CTL_BLK.TXT_BAL_I:=NULL;
			:CTL_BLK.DISPLAY_ACT_I:=NULL;
			:CTL_BLK.DISPLAY_RPT_I:=NULL;
			:CTL_BLK.DISPLAY_BAL_I:=NULL;

 			IF V_TEMP>0 THEN
 				 			 		
 				SELECT ACTUAL,REPORTED,BALANCE INTO :CTL_BLK.TXT_ACTUAL_I ,:CTL_BLK.TXT_RPT_I,:CTL_BLK.TXT_BAL_I
      		FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=:CTL_BLK.TXT_TIMESTAMP_I AND FURNACE='I'; 
      					 --#####
      			     SELECT sum(ACTUAL),sum(REPORTED) into :CTL_BLK.TXT_ACTUAL_I_TD ,:CTL_BLK.TXT_RPT_I_TD
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_I,'MON') AND TIMESTAMP<=:CTL_BLK.TXT_TIMESTAMP_I AND FURNACE='I';
      			     --#####
       SELECT BALANCE INTO :Global.vBalance_I FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=(:CTL_BLK.TXT_TIMESTAMP_H)-1 AND FURNACE='I';	
 			ELSE
 				
				Select SUM(NET_WT) into :CTL_BLK.TXT_ACTUAL_I  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:CTL_BLK.TXT_TIMESTAMP_I+6/24 and LADLE_FLEND_TIME<:CTL_BLK.TXT_TIMESTAMP_I+1+6/24 
							and DESTINATION<>'R' and fur_name='I';
			
				SELECT SUM(NVL(ACTUAL,0))-sum(NVL(REPORTED,0)) INTO :CTL_BLK.TXT_BAL_I FROM 
					DEMO.T_BF_PRODUCTION_TRACKING 
						WHERE TIMESTAMP>=TRUNC(:CTL_BLK.TXT_TIMESTAMP_I,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_I AND FURNACE='I'; 			
			
		  	:CTL_BLK.TXT_RPT_I:=nvl(:CTL_BLK.TXT_ACTUAL_I,0)+nvl(:CTL_BLK.TXT_BAL_I,0);	
		  	:Global.vBalance_I:=:CTL_BLK.TXT_BAL_I;
				:CTL_BLK.TXT_BAL_I:=NVL(:CTL_BLK.TXT_ACTUAL_I,0)-NVL(:CTL_BLK.TXT_RPT_I,0)+NVL(:Global.vBalance_I,0);		 
				
								--#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_I,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_I AND FURNACE='I';
      			     :CTL_BLK.TXT_ACTUAL_I_TD:=nvl(vActual_TD,0)+ nvl(:CTL_BLK.TXT_ACTUAL_I ,0);
      			     :CTL_BLK.TXT_RPT_I_TD:=nvl(vReported_TD,0)+ nvl(:CTL_BLK.TXT_RPT_I ,0); 
      			     	 
      			     --#####	   		  			
 			END IF;
 
		:CTL_BLK.DISPLAY_ACT_I:=nvl(:CTL_BLK.DISPLAY_ACT_G,0)+nvl(:CTL_BLK.TXT_ACTUAL_H,0)+nvl(:CTL_BLK.TXT_ACTUAL_I,0);
		:CTL_BLK.DISPLAY_RPT_I:=nvl(:CTL_BLK.DISPLAY_RPT_G,0)+nvl(:CTL_BLK.TXT_RPT_H,0)+nvl(:CTL_BLK.TXT_RPT_I,0);
		:CTL_BLK.DISPLAY_BAL_I:=nvl(:CTL_BLK.DISPLAY_BAL_G,0)+nvl(:CTL_BLK.TXT_BAL_H,0)+nvl(:CTL_BLK.TXT_BAL_I,0);

		--#####
		:CTL_BLK.DISPLAY_ACT_I_TD:=nvl(:CTL_BLK.DISPLAY_ACT_G_TD,0)+nvl(:CTL_BLK.TXT_ACTUAL_H_TD,0)+nvl(:CTL_BLK.TXT_ACTUAL_I_TD,0);
		:CTL_BLK.DISPLAY_RPT_I_TD:=nvl(:CTL_BLK.DISPLAY_RPT_G_TD,0)+nvl(:CTL_BLK.TXT_RPT_H_TD,0)+nvl(:CTL_BLK.TXT_RPT_I_TD,0);     			    
		--#####
		
									If :CTL_BLK.TXT_ACTUAL_I_TD=0 Then
      			     		:CTL_BLK.TXT_ACTUAL_I_TD:=Null;
      			     	End If;   
      			     	If :CTL_BLK.TXT_RPT_I_TD=0 Then
      			     		 :CTL_BLK.TXT_RPT_I_TD:=Null;
      			     	End If;  
 
 
 ---------------------------------------------------------------------------------------------------------------------     			     	
      			     	
      			     	
      			     	
      			     	
		If :Global.UserName like '%GBF%' Then				
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
		               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='G';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD+:BLK_CONTROL.NOOFTP_G;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_G,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_G,0);
			  :BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_G,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_G,0);
				:BLK_CONTROL.D_FUR:='G';
		ElsIf  :Global.UserName like '%HBF%' Then
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='H';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_H,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_H,0);
				:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_H,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_H,0);
				:BLK_CONTROL.D_FUR:='H';
		ElsIf  :Global.UserName like '%IBF%' Then
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='I';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_I,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_I,0);
				:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_I,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_I,0);
				:BLK_CONTROL.D_FUR:='I';
		Else
        select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD                     
		               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='A-F';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD+:BLK_CONTROL.NOOFTP;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL,0);
		  	:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL,0);
				:BLK_CONTROL.D_FUR:='A - F';
		End If;		
		
		Begin
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AG,:BLK_CONTROL.LD2_ACT_TD_AG,:BLK_CONTROL.LD3_ACT_TD_AG,:BLK_CONTROL.MRD_ACT_TD_AG from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AH,:BLK_CONTROL.LD2_ACT_TD_AH,:BLK_CONTROL.LD3_ACT_TD_AH,:BLK_CONTROL.MRD_ACT_TD_AH from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AI,:BLK_CONTROL.LD2_ACT_TD_AI,:BLK_CONTROL.LD3_ACT_TD_AI,:BLK_CONTROL.MRD_ACT_TD_AI from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H','I');
		Exception
			When Others Then
				Message(SQLERRM);
		End;
		
END;

           
	       
