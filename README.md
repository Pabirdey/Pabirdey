  vday:=to_char(to_date(:ctl_blk.ctl_date_time_prod),'DD');
		     if vday=1 then	
		     	  :BLK_CONTROL.BALANCE_C:=NVL(:BLK_CONTROL.ACTUAL_C,0)-NVL(:BLK_CONTROL.REPORTED_C,0)+0;	  
		     	
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
				   SELECT SUM(NVL(ACTUAL,0)-NVL(REPORTED,0))INTO VBAL FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=
					      TRUNC(:BLK_CONTROL.DATE_TIME_PROD_C,'MON') AND TIMESTAMP<:BLK_CONTROL.DATE_TIME_PROD_C AND FURNACE=:BLK_CONTROL.FURNACE_C;
					      :BLK_CONTROL.BALANCE_C:=NVL(:BLK_CONTROL.ACTUAL_C,0)-NVL(:BLK_CONTROL.REPORTED_C,0)+NVL(VBAL,0);
					
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
