	Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) 
    into :BLK_CONTROL.LD1_ACT_TD_AG,:BLK_CONTROL.LD2_ACT_TD_AG,:BLK_CONTROL.LD3_ACT_TD_AG,:BLK_CONTROL.MRD_ACT_TD_AG 
    from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) 
            into :BLK_CONTROL.LD1_ACT_TD_AH,:BLK_CONTROL.LD2_ACT_TD_AH,:BLK_CONTROL.LD3_ACT_TD_AH,:BLK_CONTROL.MRD_ACT_TD_AH 
            from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H');
			Select sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL) 
            into :BLK_CONTROL.LD1_ACT_TD_AI,:BLK_CONTROL.LD2_ACT_TD_AI,:BLK_CONTROL.LD3_ACT_TD_AI,:BLK_CONTROL.MRD_ACT_TD_AI 
            from demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<=:ctl_blk.ctl_date_time_prod and plant in ('A-F','G','H','I');                              
            	select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
		               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='G';	                            
                            	select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='H';	                                
                                		select sum(NOOFTP),sum(LD1_TONS_ACTUAL),sum(LD2_TONS_ACTUAL),sum(LD3_TONS_ACTUAL),sum(MRDTP_TONS_ACTUAL)
		           into vNO_TP_TD,vLD1_TONS_ACTUAL_TD,vLD2_TONS_ACTUAL_TD,vLD3_TONS_ACTUAL_TD,vMRD_TONS_ACTUAL_TD		                      
			               		FROM demo.t_ladle where date_time>=trunc(:ctl_blk.ctl_date_time_prod,'MON') and date_time<:ctl_blk.ctl_date_time_prod and Plant='I';
