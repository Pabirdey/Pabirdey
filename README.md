Declare
	P_Sum Number;
Begin

		P_Sum:=nvl(:BLK_CLAY.P1,0)+nvl(:BLK_CLAY.P2,0)+nvl(:BLK_CLAY.P3,0);		
   	--Message('P_Sum: '||P_Sum);	
		If P_Sum=100 Then			
				If :BLK_CLAY.MG_CLAY1 is Not Null and :BLK_CLAY.MG_CLAY2 is Null and :BLK_CLAY.MG_CLAY3 is Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY1||'('||:BLK_CLAY.P1||'%)';
				End If;
				If :BLK_CLAY.MG_CLAY1 is Not Null and :BLK_CLAY.MG_CLAY2 is Not Null and :BLK_CLAY.MG_CLAY3 is Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY1||'('||:BLK_CLAY.P1||'%)+'||:BLK_CLAY.MG_CLAY2||'('||:BLK_CLAY.P2||'%)';
				End If;
				If :BLK_CLAY.MG_CLAY1 is Not Null and :BLK_CLAY.MG_CLAY2 is Not Null and :BLK_CLAY.MG_CLAY3 is Not Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY1||'('||:BLK_CLAY.P1||'%)+'||:BLK_CLAY.MG_CLAY2||'('||:BLK_CLAY.P2||'%)+'||:BLK_CLAY.MG_CLAY3||'('||:BLK_CLAY.P3||'%)';
				End If;
				
				If :BLK_CLAY.MG_CLAY1 is Null and :BLK_CLAY.MG_CLAY2 is Not Null and :BLK_CLAY.MG_CLAY3 is Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY2||'('||:BLK_CLAY.P2||'%)';
				End If;
				If :BLK_CLAY.MG_CLAY1 is Null and :BLK_CLAY.MG_CLAY2 is Not Null and :BLK_CLAY.MG_CLAY3 is Not Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY2||'('||:BLK_CLAY.P2||'%)+'||:BLK_CLAY.MG_CLAY3||'('||:BLK_CLAY.P3||'%)';
				End If;
				
				If :BLK_CLAY.MG_CLAY1 is Null and :BLK_CLAY.MG_CLAY2 is Null and :BLK_CLAY.MG_CLAY3 is Not Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY3||'('||:BLK_CLAY.P3||'%)';
				End If;
				If :BLK_CLAY.MG_CLAY1 is Not Null and :BLK_CLAY.MG_CLAY2 is Null and :BLK_CLAY.MG_CLAY3 is Not Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=:BLK_CLAY.MG_CLAY1||'('||:BLK_CLAY.P1||'%)+'||:BLK_CLAY.MG_CLAY3||'('||:BLK_CLAY.P3||'%)';
				End If;
				
				If :BLK_CLAY.MG_CLAY1 is Null and :BLK_CLAY.MG_CLAY2 is Null and :BLK_CLAY.MG_CLAY3 is Null Then
						:T_CAST_DETAILS.MG_CLAY_USED:=Null;
				End If;
				
				Go_Item('T_CAST_DETAILS.MG_CLAY_USED');
				Go_Item('T_FUR_MSTR.PC_SAVE');
				Execute_Trigger('WHEN-BUTTON-PRESSED');
				Hide_Window('MG_CLAY');
		Else
				Message('Sum of Percentage is '||P_Sum||'. It should be 100.');
				Message('Sum of Percentage is '||P_Sum||'. It should be 100.');
		End If;	

Exception
	When Others Then Null;
End;
