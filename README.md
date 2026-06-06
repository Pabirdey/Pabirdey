Declare 
	v_lfe_time number;	
  v_timestamp Date;		
Begin
			Begin	
					
							FIRST_RECORD;	
					     for i in (Select ARRIVED_FROM,TRP_NO From imtg.T_GRANSHOT_DETAILS Where Timestamp=:T_LADLE_MASTER.TXTDT And SHIFT=:T_LADLE_MASTER.TXTSHIFT 
					      and AREA=:T_LADLE_MASTER.TXTFUR  Order by LADLE_FLEND_TIME)					     
				     	 Loop					     	
							   	GO_Block('T_HOT_METAL_ANAL');								   					    			
						    		   For k in (Select * From imtg.T_HOT_METAL_ANAL Where Date_Time<=(Select Max(Date_Time) From imtg.T_HOT_METAL_ANAL 
													Where FUR_NO=Decode(i.ARRIVED_FROM,'C',3,'D',4,'E',5,'F',6,'G',7,'H',8,'I',9) AND TRP_NO=i.TRP_NO 
													AND Date_Time<=to_date(to_char(:T_LADLE_DETAILS.LADLE_FLEND_TIME,'DD-MON-YY HH24:MI:SS'),'DD-MON-YY HH24:MI:SS')) AND ROWNUM=1 Order by Date_Time Desc )														
						    			 Loop				
						    			 							    			 				    			 						    		    			 							    										    			 							    			 	
						    				  :T_HOT_METAL_ANAL.CASTNO:=k.CASTNO;
						    					:T_HOT_METAL_ANAL.TP:=k.TRP_NO;
						    					:T_HOT_METAL_ANAL.HOTMETAL_TIME:=k.DATE_TIME;
						    					:T_HOT_METAL_ANAL.C:=k.C;
						    					:T_HOT_METAL_ANAL.SI:=k.SI;
						    					:T_HOT_METAL_ANAL.S:=k.S;
						    					:T_HOT_METAL_ANAL.MN:=k.MN;
						    					:T_HOT_METAL_ANAL.TI:=k.TI;
						    					:T_HOT_METAL_ANAL.P:=k.P;
						    					:T_HOT_METAL_ANAL.CR:=k.CR;
						    	    		:T_HOT_METAL_ANAL.BORON:=k.BORON;						     
						    			 End Loop;							    
								NEXT_RECORD;								  								
				     	 End Loop;
				     	FIRST_RECORD;					   	
				Exception
 			  When Others Then 
 			  DBMS_OUTPUT.PUT_LINE(SQLERRM);
 			  DBMS_OUTPUT.PUT_LINE(SQLERRM);    
				End ;
			

go_item('T_LADLE_MASTER.EXIT');
Exception
When Others Then Null;  
End;
