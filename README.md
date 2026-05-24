	select count(*) into VCount from DEMO.T_LADLE Where DATE_TIME=:BLK_CONTROL.DATE_TIME_PROD_F and Plant='A-F';
			if VCount>0 then
				 UPDATE DEMO.T_LADLE SET DATE_TIME=:BLK_CONTROL.DATE_TIME,
				        LD1_TONS=:BLK_CONTROL.LD1_TONS,LD2_TONS=:BLK_CONTROL.LD2_TONS,LD3_TONS=:BLK_CONTROL.LD3_TONS,
				        MRDTP_TONS=:BLK_CONTROL.MRDTP_TONS,NOOFTP=:BLK_CONTROL.NOOFTP
				  WHERE DATE_TIME=:BLK_CONTROL.DATE_TIME_PROD_F and Plant='A-F';
			ELSE
				  INSERT INTO DEMO.T_LADLE(DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,
				         MRDTP_TONS_ACTUAL,PLANT)
				         VALUES(:BLK_CONTROL.DATE_TIME,:BLK_CONTROL.LD1_TONS,:BLK_CONTROL.LD2_TONS,:BLK_CONTROL.LD3_TONS,:BLK_CONTROL.MRDTP_TONS,
				                :BLK_CONTROL.NOOFTP,:BLK_CONTROL.LD1_TONS_ACTUAL,:BLK_CONTROL.LD2_TONS_ACTUAL,:BLK_CONTROL.LD3_TONS_ACTUAL,
					              :BLK_CONTROL.MRDTP_TONS_ACTUAL,'A-F');
			END IF;	
            
            	 Begin
			 
   		select nooftp,noofot into vTotalTP, vTotalOT from demo.t_ladle where date_time=:BLK_CONTROL.DATE_TIME and Plant='A-F';
			Exception
  			When Others Then
       		vTotalTP:=Null;
       		vTotalOT:=Null;
			End;

			Begin
				Select sum(Net_Wt) into vTotProdTP From Demo.T_Ladle_Details Where Timestamp=:BLK_CONTROL.DATE_TIME and Trp_No<51;  			
  					 
			Exception
	 			When Others Then
       		vTotProdTP:=Null;
			End;
			
			begin			
				vHMT_TP:=Round((vTotProdTP/vTotalTP),2);
			exception
				when others then
					vHMT_TP:=null;
			end;
			
			Begin
				Select sum(Net_Wt) into vTotProdOT From Demo.T_Ladle_Details Where Timestamp=:BLK_CONTROL.DATE_TIME and Trp_No>50;
  					 
			Exception
	 			When Others Then
       		vTotProdOT:=Null;
			End;
			
			begin			
				vHMT_OT:=Round((vTotProdOT/vTotalOT),2);
			exception
				when others then
					vHMT_OT:=null;
			end;
		
			 update demo.t_ladle set HM_TONS_PER_OT=vHMT_OT, HM_TONS_PER_TP=vHMT_TP where date_time=:BLK_CONTROL.DATE_TIME and Plant='A-F';     
			COMMIT;
			
			Begin
						demo.proc_ladle_todate(:BLK_CONTROL.DATE_TIME_PROD_C);
			exception
				when others then
					Null;
			End;
