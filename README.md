Declare
	 VHours  Number;
	 vProdRateA Number;
	 vProdRateB Number;
	 vProdRateC Number;
	 vProdRateD Number;
	 vProdRateE Number;
	 vProdRateF Number;
	 vProdRateG Number;
	 vProdRateH Number;
	 vProdRateI Number;
	 vProdRateA_F Number;
	 vProdRateA_I Number;
	 CurrHrs     Number;
	 vDate   Date;
	BEGIN
	 :SYSTEM.MESSAGE_LEVEL:=25;
	    Declare
					Cursor CUR_SUM is 
					  Select fur_name,destination,ROUND(SUM(NET_WT),2) NETWT
 						        from demo.t_ladle_details
                            Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
                            			Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24  ---and fill_status>0.25
                            group by fur_name,destination;     	   
	    Begin
	    	
	    
	     		For REC_CUR_SUM in CUR_SUM LOOP	     			
	     					If REC_CUR_SUM.FUR_NAME='A' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1A:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='A' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2A:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If; 
	     						If REC_CUR_SUM.FUR_NAME='A' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3A:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If; 
	     					 If REC_CUR_SUM.FUR_NAME='A' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDA:=NVL(REC_CUR_SUM.NETWT,0);		
	     					 End If; 
	     					 If REC_CUR_SUM.FUR_NAME='A' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRA:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If; 
	     					-- For 'B'
	     					If REC_CUR_SUM.FUR_NAME='B' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1B:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='B' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2B:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='B' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3B:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='B' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDB:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='B' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRB:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
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
	     					-- For 'D'
	     					If REC_CUR_SUM.FUR_NAME='D' and REC_CUR_SUM.DESTINATION='LD1' Then
	    						 			:CTR_BLK.LD1D:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='D' and REC_CUR_SUM.DESTINATION='LD2' Then
	    						 			:CTR_BLK.LD2D:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='D' and REC_CUR_SUM.DESTINATION='LD3' Then
	    						 			:CTR_BLK.LD3D:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     					If REC_CUR_SUM.FUR_NAME='D' and REC_CUR_SUM.DESTINATION='MRD' Then
	    						 			:CTR_BLK.MRDD:=NVL(REC_CUR_SUM.NETWT,0);		
	     					End If;
	     						If REC_CUR_SUM.FUR_NAME='D' and REC_CUR_SUM.DESTINATION='GRANSHOT' Then
	    						 			:CTR_BLK.GRD:=NVL(REC_CUR_SUM.NETWT,0);		
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
	        	
	    	
	    	
	    	:CTR_BLK.LD1TOT:=NVL(:CTR_BLK.LD1A,0)+NVL(:CTR_BLK.LD1B,0)+NVL(:CTR_BLK.LD1C,0)+NVL(:CTR_BLK.LD1D,0)+ NVL(:CTR_BLK.LD1E,0)+ NVL(:CTR_BLK.LD1F,0);
	      :CTR_BLK.LD2TOT:=NVL(:CTR_BLK.LD2A,0)+NVL(:CTR_BLK.LD2B,0)+NVL(:CTR_BLK.LD2C,0)+NVL(:CTR_BLK.LD2D,0)+ NVL(:CTR_BLK.LD2E,0)+ NVL(:CTR_BLK.LD2F,0);
	      :CTR_BLK.LD3TOT:=NVL(:CTR_BLK.LD3A,0)+NVL(:CTR_BLK.LD3B,0)+NVL(:CTR_BLK.LD3C,0)+NVL(:CTR_BLK.LD3D,0)+ NVL(:CTR_BLK.LD3E,0)+ NVL(:CTR_BLK.LD3F,0);
				:CTR_BLK.MRDTOT:=NVL(:CTR_BLK.MRDA,0)+NVL(:CTR_BLK.MRDB,0)+NVL(:CTR_BLK.MRDC,0)+NVL(:CTR_BLK.MRDD,0)+ NVL(:CTR_BLK.MRDE,0)+ NVL(:CTR_BLK.MRDF,0);
				:CTR_BLK.GRTOT:=NVL(:CTR_BLK.GRA,0)+NVL(:CTR_BLK.GRB,0)+NVL(:CTR_BLK.GRC,0)+NVL(:CTR_BLK.GRD,0)+ NVL(:CTR_BLK.GRE,0)+ NVL(:CTR_BLK.GRF,0);
			
		
			
			-------------------------------  Added on 12-Feb-2008
			---- For 'A'
			Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTA
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='A' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTA:=0;
      END;
      
      ---- For 'B'
      Begin
      	Select round(SUM(NET_WT),2) into :CTR_BLK.TOTB
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='B' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTB:=0;
      END;
      ---- For 'C'
      Begin
      	Select round(SUM(NET_WT),2) into :CTR_BLK.TOTC
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='C' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTC:=0;
      END;
      ---- For 'D'
      Begin
      	Select round(SUM(NET_WT),2) into :CTR_BLK.TOTD
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='D' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTD:=0;
      END;
      
      ---- For 'E'
      Begin
      	Select round(SUM(NET_WT),2) into :CTR_BLK.TOTE
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='E' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTE:=0;
      END;
      
      ---- For 'F'
      Begin
      	Select round(SUM(NET_WT),2) into :CTR_BLK.TOTF
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='F' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTF:=0;
      END;
			--------------------------------------------------------
    	--------- For 'G'  Added on 09/02/2008
    	Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTG
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='G' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTG:=0;
      END;
			-------------------------------------
			
    	--------- For 'H'  Added on 09/02/2008
    	Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTH
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='H' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTH:=0;
      END;
			-------------------------------------
			Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTI
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='I' group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTI:=0;
      END;
     
			
				------------------------------------------------------Added for H Furnace
				:CTR_BLK.TOTH:=NVL(:CTR_BLK.LD1H,0)+ NVL(:CTR_BLK.LD2H,0)+ NVL(:CTR_BLK.LD3H,0)+ NVL(:CTR_BLK.MRDH,0);
					:CTR_BLK.TOTI:=NVL(:CTR_BLK.LD1I,0)+ NVL(:CTR_BLK.LD2I,0)+ NVL(:CTR_BLK.LD3I,0)+ NVL(:CTR_BLK.MRDI,0);
	      :CTR_BLK.LD1TOTA_I:=NVL(:CTR_BLK.LD1A,0)+NVL(:CTR_BLK.LD1B,0)+NVL(:CTR_BLK.LD1C,0)+NVL(:CTR_BLK.LD1D,0)+ NVL(:CTR_BLK.LD1E,0)+ NVL(:CTR_BLK.LD1F,0)+ NVL(:CTR_BLK.LD1G,0)+ NVL(:CTR_BLK.LD1H,0)+ NVL(:CTR_BLK.LD1I,0);
	      :CTR_BLK.LD2TOTA_I:=NVL(:CTR_BLK.LD2A,0)+NVL(:CTR_BLK.LD2B,0)+NVL(:CTR_BLK.LD2C,0)+NVL(:CTR_BLK.LD2D,0)+ NVL(:CTR_BLK.LD2E,0)+ NVL(:CTR_BLK.LD2F,0)+ NVL(:CTR_BLK.LD2G,0)+ NVL(:CTR_BLK.LD2H,0)+ NVL(:CTR_BLK.LD2I,0);
	      :CTR_BLK.LD3TOTA_I:=NVL(:CTR_BLK.LD3A,0)+NVL(:CTR_BLK.LD3B,0)+NVL(:CTR_BLK.LD3C,0)+NVL(:CTR_BLK.LD3D,0)+ NVL(:CTR_BLK.LD3E,0)+ NVL(:CTR_BLK.LD3F,0)+ NVL(:CTR_BLK.LD3G,0)+ NVL(:CTR_BLK.LD3H,0)+ NVL(:CTR_BLK.LD3I,0);
				:CTR_BLK.MRDTOTA_I:=NVL(:CTR_BLK.MRDA,0)+NVL(:CTR_BLK.MRDB,0)+NVL(:CTR_BLK.MRDC,0)+NVL(:CTR_BLK.MRDD,0)+ NVL(:CTR_BLK.MRDE,0)+ NVL(:CTR_BLK.MRDF,0)+ NVL(:CTR_BLK.MRDG,0)+ NVL(:CTR_BLK.MRDH,0)+ NVL(:CTR_BLK.MRDI,0);
				:CTR_BLK.GRTOTA_I:=NVL(:CTR_BLK.GRA,0)+NVL(:CTR_BLK.GRB,0)+NVL(:CTR_BLK.GRC,0)+NVL(:CTR_BLK.GRD,0)+ NVL(:CTR_BLK.GRE,0)+ NVL(:CTR_BLK.GRF,0)+ NVL(:CTR_BLK.GRG,0)+ NVL(:CTR_BLK.GRH,0)+ NVL(:CTR_BLK.GRI,0);	      
	      :CTR_BLK.ALLTOT :=NVL(:CTR_BLK.TOTA,0)+NVL(:CTR_BLK.TOTB,0)+NVL(:CTR_BLK.TOTC,0)+NVL(:CTR_BLK.TOTD,0)+NVL(:CTR_BLK.TOTE,0)+NVL(:CTR_BLK.TOTF,0);
	      :CTR_BLK.ALLTOTA_I:=NVL(:CTR_BLK.ALLTOT,0)+NVL(:CTR_BLK.TOTG,0)+NVL(:CTR_BLK.TOTH,0)+NVL(:CTR_BLK.TOTI,0);
	      ----------------------------------------------------------------------------
	     
	      	--------------------------------------------------------
    	--------- For 'H'  Added on 17/05/2008
    	Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTH
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='H'  group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTH:=0;
      END;
      ------------------------------------------------------
      	Begin
				Select round(SUM(NET_WT),2) into :CTR_BLK.TOTI
      	from demo.t_ladle_details Where Ladle_FlEnd_Time>=trunc(:t_ladle_master.txtdt)+6/24 and 
      	Ladle_FlEnd_Time<(trunc(:t_ladle_master.txtdt)+1)+6/24
      	and fur_name='I'  group by fur_name;
      Exception
      	when others then
      	:CTR_BLK.TOTI:=0;
      END;
			-------------------------------------
	      
	      If :t_ladle_master.txtshift<>'C' Then 
	       		VHours:=to_number(to_char(sysdate,'hh24'))-6;
	       		vDate:=Trunc(Sysdate);
	      Else
	      	 CurrHrs:=to_number(to_char(sysdate,'hh24'));
	      	 --VHours:=to_number(to_char(sysdate,'hh24'))-6;
	      	 If CurrHrs>=0 and CurrHrs<6 Then
	      	 			vHours:=18+CurrHrs;
	      	 			vDate:=Trunc(Sysdate)-1;
	      	 Else
	      	 	    VHours:=to_number(to_char(sysdate,'hh24'))-6;
	      	 	    vDate:=Trunc(Sysdate);
	      	 End If;
	      	 
	      End If;
	    
	     If VHours=0 then VHours:=1; 
	     end if;
	      
	     --If :T_LADLE_MASTER.TXTDT>=Trunc(Sysdate) Then  
	     If :T_LADLE_MASTER.TXTDT=vDate Then  	
	       vProdRateA:= :CTR_BLK.TOTA/vHours;
	     	:CTR_BLK.EPRODA:=round(:CTR_BLK.TOTA+vProdRateA*(24-vHours),1);
	     	
	     	 vProdRateB:= :CTR_BLK.TOTB/vHours;
	     	:CTR_BLK.EPRODB:=round(:CTR_BLK.TOTB+vProdRateB*(24-vHours),1);
	     	
	     	 vProdRateC:= :CTR_BLK.TOTC/vHours;
	     	:CTR_BLK.EPRODC:=round(:CTR_BLK.TOTC+vProdRateC*(24-vHours),1);
	     	
	     	 vProdRateD:= :CTR_BLK.TOTD/vHours;
	     	:CTR_BLK.EPRODD:=round(:CTR_BLK.TOTD+vProdRateD*(24-vHours),1);
	     	
	     	 vProdRateE:= :CTR_BLK.TOTE/vHours;
	     	:CTR_BLK.EPRODE:=round(:CTR_BLK.TOTE+vProdRateE*(24-vHours),1);
	     	
	     	 vProdRateF:= :CTR_BLK.TOTF/vHours;
	     	:CTR_BLK.EPRODF:=round(:CTR_BLK.TOTF+vProdRateF*(24-vHours),1);
	     	
	     	 vProdRateG:= :CTR_BLK.TOTG/vHours;
	     	:CTR_BLK.EPRODG:=round(:CTR_BLK.TOTG+vProdRateG*(24-vHours),1);
	     	
	     	--------------------------------------------------------------- Added for H Furnace
	     	 vProdRateH:= :CTR_BLK.TOTH/vHours;
	     	:CTR_BLK.EPRODH:=round(:CTR_BLK.TOTH+vProdRateH*(24-vHours),1);
	     	---------------------------------------------------------------------
	     	vProdRateI:= :CTR_BLK.TOTI/vHours;
	     	:CTR_BLK.EPRODI:=round(:CTR_BLK.TOTI+vProdRateI*(24-vHours),1);
	     	---------------------------------------------------------------
	     Else
	     	:CTR_BLK.EPRODA:=:CTR_BLK.TOTA;
	     	:CTR_BLK.EPRODB:=:CTR_BLK.TOTB;
	     	:CTR_BLK.EPRODC:=:CTR_BLK.TOTC;
	     	:CTR_BLK.EPRODD:=:CTR_BLK.TOTD;
	     	:CTR_BLK.EPRODE:=:CTR_BLK.TOTE;
	     	:CTR_BLK.EPRODF:=:CTR_BLK.TOTF;
	     	:CTR_BLK.EPRODG:=:CTR_BLK.TOTG;	     	
	     	:CTR_BLK.EPRODH:=:CTR_BLK.TOTH;  -- Added for H Furnace
	     	:CTR_BLK.EPRODI:=:CTR_BLK.TOTI;
	     End If;	
	     	
	     	:CTR_BLK.ALLEPROD:=:CTR_BLK.EPRODA+:CTR_BLK.EPRODB+:CTR_BLK.EPRODC+:CTR_BLK.EPRODD+:CTR_BLK.EPRODE+:CTR_BLK.EPRODF;
	      --:CTR_BLK.ALLEPRODA_G:=:CTR_BLK.EPRODA+:CTR_BLK.EPRODB+:CTR_BLK.EPRODC+:CTR_BLK.EPRODD+:CTR_BLK.EPRODE+:CTR_BLK.EPRODF+:CTR_BLK.EPRODG;
	      
	      ----------------------- Added for H Furnace
	      :CTR_BLK.ALLEPRODA_I:=:CTR_BLK.EPRODA+:CTR_BLK.EPRODB+:CTR_BLK.EPRODC+:CTR_BLK.EPRODD+:CTR_BLK.EPRODE+:CTR_BLK.EPRODF+:CTR_BLK.EPRODG+:CTR_BLK.EPRODH+:CTR_BLK.EPRODI;		
	      -----------------------
	     End;
	 
	     --If Item Value is Null  
       If :CTR_BLK.LD1A is NULL Then 
        	    :CTR_BLK.LD1A:=0 ;
        End If;
        If :CTR_BLK.LD2A is NULL Then 
        	    :CTR_BLK.LD2A:=0 ;
        End If;
         If :CTR_BLK.LD3A is NULL Then 
        	    :CTR_BLK.LD3A:=0 ;
        End If;
        If :CTR_BLK.MRDA is NULL Then 
        	    :CTR_BLK.MRDA:=0 ;
        End If;
        If :CTR_BLK.LD1B is NULL Then 
        	    :CTR_BLK.LD1B:=0 ;
        End If;
        If :CTR_BLK.LD2B is NULL Then 
        	    :CTR_BLK.LD2B:=0 ;
        End If;
        If :CTR_BLK.LD3B is NULL Then 
        	    :CTR_BLK.LD3B:=0 ;
        End If;
        If :CTR_BLK.MRDB is NULL Then 
        	    :CTR_BLK.MRDB:=0 ;
        End If;
        If :CTR_BLK.LD1C is NULL Then 
        	    :CTR_BLK.LD1C:=0 ;
        End If;
        If :CTR_BLK.LD2C is NULL Then 
        	    :CTR_BLK.LD2C:=0 ;
        End If;
        If :CTR_BLK.LD3C is NULL Then 
        	    :CTR_BLK.LD3C:=0 ;
        End If;
        If :CTR_BLK.MRDC is NULL Then 
        	    :CTR_BLK.MRDC:=0 ;
        End If;
        If :CTR_BLK.LD1D is NULL Then 
        	    :CTR_BLK.LD1D:=0 ;
        End If;
        If :CTR_BLK.LD2D is NULL Then 
        	    :CTR_BLK.LD2D:=0 ;
        End If;
        If :CTR_BLK.LD3D is NULL Then 
        	    :CTR_BLK.LD3D:=0 ;
        End If;
        If :CTR_BLK.MRDD is NULL Then 
        	    :CTR_BLK.MRDD:=0 ;
        End If;
        If :CTR_BLK.LD1E is NULL Then 
        	    :CTR_BLK.LD1E:=0 ;
        End If;
        If :CTR_BLK.LD2E is NULL Then 
        	    :CTR_BLK.LD2E:=0 ;
        End If;
        If :CTR_BLK.LD3E is NULL Then 
        	    :CTR_BLK.LD3E:=0 ;
        End If;
        If :CTR_BLK.MRDE is NULL Then 
        	    :CTR_BLK.MRDE:=0 ;
        End If;
        If :CTR_BLK.LD1F is NULL Then 
        	    :CTR_BLK.LD1F:=0 ;
        End If;
        If :CTR_BLK.LD2F is NULL Then 
        	    :CTR_BLK.LD2F:=0 ;
        End If;
        If :CTR_BLK.LD3F is NULL Then 
        	    :CTR_BLK.LD3F:=0 ;
        End If;
        If :CTR_BLK.MRDF is NULL Then 
        	    :CTR_BLK.MRDF:=0 ;
        End If;
        If :CTR_BLK.LD1G is NULL Then 
        	    :CTR_BLK.LD1G:=0 ;
        End If;
        If :CTR_BLK.LD2G is NULL Then 
        	    :CTR_BLK.LD2G:=0 ;
        End If;
        If :CTR_BLK.LD3G is NULL Then 
        	    :CTR_BLK.LD3G:=0 ;
        End If;
        If :CTR_BLK.MRDG is NULL Then 
        	    :CTR_BLK.MRDG:=0 ;
        End If;
        
        ------------------------------- Added for H Furnace
        If :CTR_BLK.LD1H is NULL Then 
        	    :CTR_BLK.LD1H:=0 ;
        End If;
        If :CTR_BLK.LD2H is NULL Then 
        	    :CTR_BLK.LD2H:=0 ;
        End If;
         If :CTR_BLK.LD3H is NULL Then 
        	    :CTR_BLK.LD3H:=0 ;
        End If;
        If :CTR_BLK.MRDH is NULL Then 
        	    :CTR_BLK.MRDH:=0 ;
        End If;
        ------------------------------
         If :CTR_BLK.LD1I is NULL Then 
        	    :CTR_BLK.LD1I:=0 ;
        End If;
        If :CTR_BLK.LD2I is NULL Then 
        	    :CTR_BLK.LD2I:=0 ;
        End If;
         If :CTR_BLK.LD3I is NULL Then 
        	    :CTR_BLK.LD3I:=0 ;
        End If;
        If :CTR_BLK.MRDI is NULL Then 
        	    :CTR_BLK.MRDI:=0 ;
        End If;
        -------------------------------
        
        If  :CTR_BLK.ALLTOT is NULL Then 
        			:CTR_BLK.ALLTOT:=0 ;
        End If;	   
        
        :Global.New_SlNo := 1;
        EXCEPTION 
        	WHEN OTHERS THEN
        	   NULL;
			       --	MESSAGE(SQLERRM||'  '||SQLCODE);
			       --	MESSAGE(SQLERRM||'  '||SQLCODE);
END;
