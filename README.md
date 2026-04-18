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
						
