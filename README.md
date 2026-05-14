
		
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
