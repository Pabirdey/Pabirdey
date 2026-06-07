Cursor CUR_SUM is 
					  Select fur_name,destination,ROUND(SUM(NET_WT),2) NETWT
 						        from demo.t_ladle_details
                            Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
                            			Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24  ---and fill_status>0.25
                            group by fur_name,destination;     	   
	    Begin
	    	
	    
	     		For REC_CUR_SUM in CUR_SUM LOOP	     			
	     					
	     					-- For 'C'
	     					If REC_CUR_SUM.FUR_NAME='C' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1C:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='C' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2C:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='C' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3C:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					
	     					If REC_CUR_SUM.FUR_NAME='C' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDC:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='C' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRC:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					
	     					-- For 'E'
	     					If REC_CUR_SUM.FUR_NAME='E' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1E:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='E' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2E:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='E' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3E:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='E' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDE:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='E' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRE:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					-- For 'F'
	     					If REC_CUR_SUM.FUR_NAME='F' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1F:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='F' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2F:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='F' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3F:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='F' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDF:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='F' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRF:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					
	     					-- For 'G'
	     					If REC_CUR_SUM.FUR_NAME='G' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1G:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='G' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2G:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='G' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3G:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='G' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDG:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='G' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRG:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					-- Added for H Furnace
	     					------------------------------------------------------------------
	     					If REC_CUR_SUM.FUR_NAME='H' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1H:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='H' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2H:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='H' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3H:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='H' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDH:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='H' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRH:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					-------------------------------------------------------------------
	     	-- Added for I Furnace
	     					------------------------------------------------------------------
	     					If REC_CUR_SUM.FUR_NAME='I' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1I:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='I' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2I:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='I' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3I:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='I' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDI:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='I' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRI:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     		End Loop;
	        	
	    	
	    	
	    	:CTR_BLK.LD1TOT:=NVL(:CTR_BLK.LD1C,0)+ NVL(:CTR_BLK.LD1E,0)+ NVL(:CTR_BLK.LD1F,0);
	      :CTR_BLK.LD2TOT:=NVL(:CTR_BLK.LD2C,0)+ NVL(:CTR_BLK.LD2E,0)+ NVL(:CTR_BLK.LD2F,0);
	      :CTR_BLK.LD3TOT:=+NVL(:CTR_BLK.LD3C,0)+ NVL(:CTR_BLK.LD3E,0)+ NVL(:CTR_BLK.LD3F,0);
				:CTR_BLK.MRDTOT:=NVL(:CTR_BLK.MRDC,0)+ NVL(:CTR_BLK.MRDE,0)+ NVL(:CTR_BLK.MRDF,0);
				:CTR_BLK.GRTOT:=NVL(:CTR_BLK.GRC,0)+ NVL(:CTR_BLK.GRE,0)+ NVL(:CTR_BLK.GRF,0);
			
