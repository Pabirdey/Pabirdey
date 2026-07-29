	
    Begin
    select nooftp,noofot into vTotalTP, vTotalOT from demo.t_ladle where date_time=:BLK_CONTROL.DATE_TIME and Plant='A-F';
			Exception
  			When Others Then
       		vTotalTP:=Null;
       		vTotalOT:=Null;
			End;
            
            	Begin
			
  			Select sum(Net_Wt) into vTotProdTP From Demo.T_Ladle_Details Where Timestamp=:BLK_CONTROL.DATE_TIME and Trp_No<52;  			
  					 
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
			
  			Select sum(Net_Wt) into vTotProdOT From Demo.T_Ladle_Details Where Timestamp=:BLK_CONTROL.DATE_TIME and Trp_No>51;
  					 
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
