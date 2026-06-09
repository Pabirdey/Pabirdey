Declare
v_Pouring_rate number(15,3);
v_lfe_time number;
v_timestamp date;
v_timestamp1 date;
v_lst_date date;
Begin
   									    
  					   		v_lfe_time:=to_number(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'hh24'));
  					   		v_lst_date:=to_date(:T_LADLE_DETAILS.LADLE_FLST_TIME,'DD-mon-yyyy HH24:MI');
  					   		
  					   		If v_lfe_time>=6 and v_lfe_time<14 Then  					   		
  					   				If :T_LADLE_MASTER.TXTSHIFT='C' Then
  					   						v_timestamp:=to_date(to_char(:T_LADLE_MASTER.TXTDT,'DD-MON-YYYY'),'DD-MON-YYYY')+1;  					   				
  					   				Else
  					   						v_timestamp:=:T_LADLE_MASTER.TXTDT;
  					   				End If;
  					   		ElsIf v_lfe_time>=14 and v_lfe_time<22 Then  					   		
  					   					v_timestamp:=:T_LADLE_MASTER.TXTDT;
  					   		ElsIf v_lfe_time>=22 and v_lfe_time<=24 Then  					   			
  					   					v_timestamp:=:T_LADLE_MASTER.TXTDT;
  					   		ElsIf v_lfe_time>=0 and v_lfe_time<6 Then  					   			
  					   					v_timestamp:=to_date(to_char(:T_LADLE_MASTER.TXTDT,'DD-MON-YYYY'),'DD-MON-YYYY')+1;  					   				
  					   		End If;
  					   
 								
  								
				  			:T_LADLE_DETAILS.GROSS_WT:=FN_GR_TARE_WT(:T_LADLE_DETAILS.TRP_NO,to_date(to_char(v_timestamp,'DD-MON-YYYY'),'DD-MON-YYYY'),to_date(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'HH24:MI'),'HH24:MI'),:T_LADLE_DETAILS.ARRIVED_FROM);	
								:T_LADLE_DETAILS.TARE_WT:=FN_TARE_WT(:T_LADLE_DETAILS.TRP_NO,to_date(to_char(v_timestamp,'DD-MON-YYYY'),'DD-MON-YYYY'),to_date(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'HH24:MI'),'HH24:MI'),:T_LADLE_DETAILS.ARRIVED_FROM);
								:T_LADLE_DETAILS.NET_WT:=FN_NET_WT(:T_LADLE_DETAILS.TRP_NO,to_date(to_char(v_timestamp,'DD-MON-YYYY'),'DD-MON-YYYY'),to_date(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'HH24:MI'),'HH24:MI'),:T_LADLE_DETAILS.ARRIVED_FROM);
								:T_LADLE_DETAILS.HMT:=FN_GRANSHOT_HMT(:T_LADLE_DETAILS.TRP_NO,to_date(to_char(v_timestamp,'DD-MON-YYYY'),'DD-MON-YYYY'),to_date(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'HH24:MI'),'HH24:MI'),:T_LADLE_DETAILS.ARRIVED_FROM);
								
						
							
									
							:T_LADLE_DETAILS.TXT_LADLEFILLINGRATE:=:T_LADLE_DETAILS.NET_WT/((:T_LADLE_DETAILS.LADLE_FLEND_TIME-:T_LADLE_DETAILS.LADLE_FLST_TIME)*1440);

							
								
								 v_Pouring_rate:=:T_LADLE_DETAILS.TXT_LADLEFILLINGRATE;	
					--	Message('LADLE_F_END_DATE'||v_Pouring_rate);
					--	Message('LADLE_F_END_DATE'||v_Pouring_rate);
											
		
		go_item('T_LADLE_MASTER.EXIT');		
	Exception
	When Others Then NUll;
	End;
	


