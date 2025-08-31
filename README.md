DECLARE
	vwrp number;
	vLD_SLAG_FINES number;
	
		vLD_Sludge_Cons    Number ;
    vMill_Scale_Cons   Number ;
    vFlue_Dust_Cons     Number ;
    vEsp_Dust_Cons      Number ;
    vMILL_SLUDGE_Cons Number;
    vKILN_DUST_Cons     Number ;
    vGcp_Sludge_Cons    Number ;
    vLIME_FINES_cons   Number ;
    vWRP_cons           Number ;
    vLD_SLAG_FINES_cons  Number ;    
    vPSW1 Number:=0;
    vPSW2 Number:=0;
    vPrep_End_Date Date;
    
BEGIN	
			If trim(:BLOCK238.LST_SOURCE)='RMBB_KNR' Then	
					
						vPrep_End_Date:=:T_PILE_RAWMAT_QUANTITY_NEW.PREP_END_DATE;
						:T_PILE_RAWMAT_QUANTITY_NEW.SOLID_WASTE:=Nvl(:BLK_PSW.TXT_PSW1,0) + Nvl(:BLK_PSW.TXT_PSW2,0);
						
						If :BLK_PSW.TXT_PSW1>0 Then
								vPSW1:=:BLK_PSW.TXT_PSW1;
								--Message('vPSW1 :'||:BLK_PSW.TXT_PSW1);
								If :BLK_PSW.LST_BL1 is null Then
									message('PSW Blend 1 can not be blank');
									message('PSW Blend 1 can not be blank');
								End If;
						End If;
						
						If :BLK_PSW.TXT_PSW2>0 Then
								vPSW2:=:BLK_PSW.TXT_PSW2;
								--Message('vPSW2 :'||:BLK_PSW.TXT_PSW2);
								If :BLK_PSW.LST_BL2 is null Then
									message('PSW Blend 2 can not be blank');
									message('PSW Blend 2 can not be blank');
								End If;
						End If;		
						
						Begin								
								
								
								Select  SUM(LD_Sludge), SUM(Mill_Scale),  SUM(Flue_Dust), SUM(Esp_Dust), SUM(Kiln_Dust), SUM(Gcp_Sludge), SUM(Lime_Fines), SUM(Wrp_MET), SUM(LD_Slag_Fines),SUM(MILL_SLUDGE)
									into vLD_Sludge_Cons, vMill_Scale_Cons, vFlue_Dust_Cons, vEsp_Dust_Cons, vKILN_DUST_Cons, vGcp_Sludge_Cons, vLIME_FINES_cons, vWRP_cons, vLD_SLAG_FINES_cons ,vMILL_SLUDGE_Cons from
								(
								Select vPSW1*Avg(LD_Sludge)/100 LD_Sludge,vPSW1*Avg(Mill_Scale)/100 Mill_Scale,vPSW1*Avg(Flue_Dust)/100 Flue_Dust,vPSW1*Avg(Esp_Dust)/100 Esp_Dust,vPSW1*Avg(Kiln_Dust)/100 Kiln_Dust,vPSW1*Avg(Gcp_Sludge)/100 Gcp_Sludge,vPSW1*Avg(Lime_Fines)/100 Lime_Fines,vPSW1*Avg(Wrp_MET)/100 Wrp_MET,vPSW1*Avg(LD_Slag_Fines)/100 LD_Slag_Fines,vPSW1*Avg(MILL_SLUDGE)/100  MILL_SLUDGE   
						            from T_PSW_DAILY where trim(SOURCE)='RMBB_KNR' and TIMESTAMP>=trunc(vPrep_End_Date)-200 and BLEND_NO=:BLK_PSW.LST_BL1
						    Union
						    	Select vPSW2*Avg(LD_Sludge)/100 LD_Sludge,vPSW2*Avg(Mill_Scale)/100 Mill_Scale,vPSW2*Avg(Flue_Dust)/100 Flue_Dust,vPSW2*Avg(Esp_Dust)/100 Esp_Dust,vPSW2*Avg(Kiln_Dust)/100 Kiln_Dust,vPSW2*Avg(Gcp_Sludge)/100 Gcp_Sludge,vPSW2*Avg(Lime_Fines)/100 Lime_Fines,vPSW2*Avg(Wrp_MET)/100 Wrp_MET,vPSW2*Avg(LD_Slag_Fines)/100 LD_Slag_Fines ,vPSW2*Avg(MILL_SLUDGE)/100 MILL_SLUDGE 
						            from T_PSW_DAILY where trim(SOURCE)='RMBB_KNR' and TIMESTAMP>=trunc(vPrep_End_Date)-200 and BLEND_NO=:BLK_PSW.LST_BL2
						    );
								
								
								--Message('vMill_Scale_Cons :'||vMill_Scale_Cons);
								
							--	:MILL_SLUDGE_PRM:=0;
								:MILL_SLUDGE_PRM:=vMILL_SLUDGE_Cons;  
								:MILL_SCALE_PRM:=vMill_Scale_Cons; 
								:LD_SLUDGE_MIX:=0;
								:LD_SLUDGE_PRM:=vLD_Sludge_Cons; 
							  :FLUE_DUST_PRM:=vFlue_Dust_Cons;
							  :ESP_DUST_PRM:=vEsp_Dust_Cons; 
							  :GCP_SLUDGE:=vGcp_Sludge_Cons;
							  :KILN_DUST_PRM:=vKILN_DUST_Cons;
							  :LIME_FINES:=vLIME_FINES_cons;
							  :WRP:=vWRP_cons;
							  :LD_SLAG_FINES:=vLD_SLAG_FINES_cons;
							  
							  Go_block('T_PILE_RAWMAT_QUANTITY_NEW');							  
							  Execute_trigger('POST-TEXT-ITEM');
							  
						Exception
							When Others Then 
								Message(SQLERRM);
								Message(SQLERRM);
						End;
			
			Else
				
						if :BLOCK238.LST_SOURCE='RMBB' OR :BLOCK238.LST_SOURCE='RMBBN' THEN
							   vwrp :=:WRP;
						     vLD_SLAG_FINES:=:LD_SLAG_FINES;
						END IF;
						
						If :PREP_START_DATE>='01-FEB-2014' Then
								If :SOLID_WASTE>0 Then	
										imtg.PROC_UPDATE_PSW_DIST(:BLOCK238.TXT_PILESRCH,:PREP_START_DATE, :PREP_END_DATE,:BLOCK238.LST_SOURCE,:SOLID_WASTE, :MILL_SLUDGE_PRM, :MILL_SCALE_PRM, :LD_SLUDGE_MIX, :LD_SLUDGE_PRM, 
							        :FLUE_DUST_PRM,:ESP_DUST_PRM, :GCP_SLUDGE,:KILN_DUST_PRM,:LIME_FINES,:WRP,:LD_SLAG_FINES);
								Else
									:MILL_SLUDGE_PRM:=Null;
									:MILL_SCALE_PRM:=Null; 
									:LD_SLUDGE_MIX:=Null;
									:LD_SLUDGE_PRM :=Null; 
									:FLUE_DUST_PRM:=Null;
									:ESP_DUST_PRM:=Null; 
									:GCP_SLUDGE:=Null;
									:KILN_DUST_PRM:=NULL;
									:LIME_FINES:=NULL;
									:WRP:=NULL;
									:LD_SLAG_FINES:=NULL;
									
								End If;
						End If;
						if :BLOCK238.LST_SOURCE='RMBB' OR :BLOCK238.LST_SOURCE='RMBBN' THEN
							   :wrp :=VWRP;
						     :LD_SLAG_FINES:=VLD_SLAG_FINES;
						END IF;
						
			End If;
END;
