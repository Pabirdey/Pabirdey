      			     	
		If :Global.UserName like '%GBF%' Then				
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
		               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='G';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD+:BLK_CONTROL.NOOFTP_G;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_G,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_G,0);
			  :BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_G,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_G,0);
				:BLK_CONTROL.D_FUR:='G';
		ElsIf  :Global.UserName like '%HBF%' Then
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='H';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_H,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_H,0);
				:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_H,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_H,0);
				:BLK_CONTROL.D_FUR:='H';
		ElsIf  :Global.UserName like '%IBF%' Then
				select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='I';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL_I,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL_I,0);
				:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL_I,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL_I,0);
				:BLK_CONTROL.D_FUR:='I';
		Else
        select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD                     
		               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='A-F';
				--:BLK_CONTROL.NO_TP_TD:=vNO_TP_TD+:BLK_CONTROL.NOOFTP;
				:BLK_CONTROL.LD1_TONS_ACTUAL_TD:=nvl(vLD1_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD1_TONS_ACTUAL,0);
				:BLK_CONTROL.LD2_TONS_ACTUAL_TD:=nvl(vLD2_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD2_TONS_ACTUAL,0);
		  	:BLK_CONTROL.LD3_TONS_ACTUAL_TD:=nvl(vLD3_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.LD3_TONS_ACTUAL,0);
				:BLK_CONTROL.MRD_TONS_ACTUAL_TD:=nvl(vMRD_TONS_ACTUAL_TD,0)+nvl(:BLK_CONTROL.MRDTP_TONS_ACTUAL,0);
				:BLK_CONTROL.D_FUR:='A - F';
		End If;		
		
		Begin
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AG,:BLK_CONTROL.LD2_ACT_TD_AG,:BLK_CONTROL.LD3_ACT_TD_AG,:BLK_CONTROL.MRD_ACT_TD_AG from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AH,:BLK_CONTROL.LD2_ACT_TD_AH,:BLK_CONTROL.LD3_ACT_TD_AH,:BLK_CONTROL.MRD_ACT_TD_AH from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) into :BLK_CONTROL.LD1_ACT_TD_AI,:BLK_CONTROL.LD2_ACT_TD_AI,:BLK_CONTROL.LD3_ACT_TD_AI,:BLK_CONTROL.MRD_ACT_TD_AI from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H','I');
		Exception
			When Others Then
				Message(SQLERRM);
		End;
		
END;
