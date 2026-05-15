 public JsonResult GET_GBF_IBF_ACTUAL_REPORT(string prodDate)
        {
            BFViewModel model =new BFViewModel();
            model.Furnaces =new List<GBFTOIBFPRODUCTION>();
            DateTime dt =Convert.ToDateTime(prodDate);
            string[] furnaces ={"G","H","I"};
            using (OracleConnection con =new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();                
                foreach (string furnace in furnaces)
                {
                    GBFTOIBFPRODUCTION row =new GBFTOIBFPRODUCTION();
                    row.FURNACE =furnace;
                    string chkQry = @"SELECT COUNT(*) FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP=:PDATE AND FURNACE=:FURNACE";
                    OracleCommand chkCmd =new OracleCommand(chkQry, con);
                    chkCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                    chkCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                    int count =Convert.ToInt32(chkCmd.ExecuteScalar());                   
                    if (count > 0)
                    {
                        string qry = @"SELECT NVL(ACTUAL,0),NVL(REPORTED,0),NVL(BALANCE,0) FROM DEMO.T_BF_PRODUCTION_TRACKING 
                                        WHERE TIMESTAMP=:PDATE AND FURNACE=:FURNACE";
                        OracleCommand cmd =new OracleCommand(qry, con);
                        cmd.Parameters.Add("PDATE",  OracleDbType.Date).Value = dt;
                        cmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                        OracleDataReader dr =cmd.ExecuteReader();
                        if (dr.Read())
                        {
                            row.ACTUAL=Convert.ToDecimal(dr[0]);
                            row.REPORTED=Convert.ToDecimal(dr[1]);
                            row.BALANCE=Convert.ToDecimal(dr[2]);
                        }
                    }
                    else
                    {                     
                        string actualQry = @"SELECT NVL(SUM(NET_WT),0) FROM DEMO.T_LADLE_DETAILS 
                                            WHERE LADLE_FLEND_TIME>=:FROMDATE AND LADLE_FLEND_TIME<:TODATE 
                                            AND DESTINATION <> 'R' AND FUR_NAME=:FURNACE";
                        OracleCommand actualCmd =new OracleCommand(actualQry, con);
                        actualCmd.Parameters.Add("FROMDATE",OracleDbType.Date).Value =dt.AddHours(6);
                        actualCmd.Parameters.Add("TODATE",OracleDbType.Date).Value =dt.AddDays(1).AddHours(6);
                        actualCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                        row.ACTUAL=Convert.ToDecimal(actualCmd.ExecuteScalar());

                        string balQry = @"SELECT NVL(SUM(NVL(ACTUAL,0)-NVL(REPORTED,0)),0) FROM DEMO.T_BF_PRODUCTION_TRACKING
                                         WHERE TIMESTAMP >=TRUNC(:PDATE,'MON') AND TIMESTAMP<:PDATE  AND FURNACE=:FURNACE";
                        OracleCommand balCmd =new OracleCommand(balQry, con);
                        balCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                        balCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                        row.BALANCE=Convert.ToDecimal(balCmd.ExecuteScalar());                       
                        row.REPORTED=row.ACTUAL+row.BALANCE;                        
                        row.BALANCE =row.ACTUAL-row.REPORTED+row.BALANCE;
                    }

                    string tdQry = @"SELECT NVL(SUM(ACTUAL),0),NVL(SUM(REPORTED),0) FROM DEMO.T_BF_PRODUCTION_TRACKING 
                                     WHERE TIMESTAMP>=TRUNC(:PDATE,'MON') AND TIMESTAMP<=:PDATE AND FURNACE = :FURNACE";
                    OracleCommand tdCmd=new OracleCommand(tdQry, con);
                    tdCmd.Parameters.Add("PDATE",OracleDbType.Date).Value = dt;
                    tdCmd.Parameters.Add("FURNACE",OracleDbType.Varchar2).Value = furnace;
                    OracleDataReader tdDr =tdCmd.ExecuteReader();

                    if (tdDr.Read())
                    {
                        row.ACTUAL_TD=Convert.ToDecimal(tdDr[0]);
                        row.REPORTED_TD=Convert.ToDecimal(tdDr[1]);
                    }
                    row.LD1_TONS=GetDestinationTotal(con,dt,furnace,"LD1");                    
                    row.LD2_TONS=GetDestinationTotal(con,dt,furnace,"LD2");                    
                    row.LD3_TONS=GetDestinationTotal(con,dt,furnace,"LD3");                    
                    row.MRDTP_TONS=GetDestinationTotal(con,dt,furnace,"MRD");                    
                    row.NOOFTP=GetTP(con,dt,furnace);  
                                      
                    model.DISPLAY_ACTUAL+=row.ACTUAL;
                    model.DISPLAY_REPORTED+=row.REPORTED;
                    model.DISPLAY_BALANCE+=row.BALANCE;
                    model.DISPLAY_ACTUAL_TD+=row.ACTUAL_TD;
                    model.DISPLAY_REPORTED_TD+=row.REPORTED_TD;                    
                    model.Furnaces.Add(row);
                }
            }

            return Json(model,JsonRequestBehavior.AllowGet);
        }

        	V_TEMP:=0;	
		select COUNT(*) INTO V_TEMP from DEMO.T_LADLE where DATE_TIME=:ctl_blk.ctl_date_time_prod and PLANT ='G'; 
		
		IF V_TEMP>0 THEN 	
			
					
 				select DATE_TIME,LD1_TONS,LD2_TONS,LD3_TONS,MRDTP_TONS,NOOFTP,LD1_TONS_ACTUAL,LD2_TONS_ACTUAL,LD3_TONS_ACTUAL,MRDTP_TONS_ACTUAL
		                into :BLK_CONTROL.DATE_TIME,:BLK_CONTROL.LD1_TONS_G,:BLK_CONTROL.LD2_TONS_G,:BLK_CONTROL.LD3_TONS_G,:BLK_CONTROL.MRDTP_TONS_G,:BLK_CONTROL.NOOFTP_G,
		                     :BLK_CONTROL.LD1_TONS_ACTUAL_G,:BLK_CONTROL.LD2_TONS_ACTUAL_G,:BLK_CONTROL.LD3_TONS_ACTUAL_G,:BLK_CONTROL.MRDTP_TONS_ACTUAL_G		                      
		                FROM demo.t_ladle where date_time=:ctl_blk.ctl_date_time_prod and Plant='G';

		                
		Else

				SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD1_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
					 AND DESTINATION='LD1' and fur_name='G';	
					:BLK_CONTROL.LD1_TONS_ACTUAL_G:=:BLK_CONTROL.LD1_TONS_G;
					
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD2_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD2' and fur_name ='G';	
					:BLK_CONTROL.LD2_TONS_ACTUAL_G:=:BLK_CONTROL.LD2_TONS_G;
						
					SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.LD3_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='LD3' and fur_name ='G';	
					:BLK_CONTROL.LD3_TONS_ACTUAL_G:=:BLK_CONTROL.LD3_TONS_G;
					
						SELECT NVL(SUM(NET_WT),0) INTO :BLK_CONTROL.MRDTP_TONS_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
						AND DESTINATION='MRD' and fur_name ='G';	
				:BLK_CONTROL.MRDTP_TONS_ACTUAL_G:=:BLK_CONTROL.MRDTP_TONS_G;
				
				SELECT NVL(SUM(FILL_STATUS),0) INTO :BLK_CONTROL.NOOFTP_G from  demo.t_ladle_details where
		 			LADLE_FLEND_TIME>=:BLK_CONTROL.DATE_TIME+6/24 and LADLE_FLEND_TIME< :BLK_CONTROL.DATE_TIME+1+6/24
							AND  TRP_NO<=50 and fur_name ='G' and ret_flag='N';
							
		End If;
		

		
		V_TEMP:=0;
		select COUNT(*) INTO V_TEMP from DEMO.T_BF_PRODUCTION_TRACKING where timestamp=:ctl_blk.ctl_date_time_prod AND FURNACE ='G';    
 		
 		:CTL_BLK.TXT_TIMESTAMP_G:=:ctl_blk.ctl_date_time_prod;
			:CTL_BLK.TXT_FURNACE_G:='G';
			:CTL_BLK.TXT_ACTUAL_G:=NULL;
			:CTL_BLK.TXT_RPT_G:=NULL;
			:CTL_BLK.TXT_BAL_G:=NULL;
			:CTL_BLK.DISPLAY_ACT_G:=NULL;
			:CTL_BLK.DISPLAY_RPT_G:=NULL;
			:CTL_BLK.DISPLAY_BAL_G:=NULL;

 			IF V_TEMP>0 THEN 			

 				SELECT ACTUAL,REPORTED,BALANCE INTO :CTL_BLK.TXT_ACTUAL_G ,:CTL_BLK.TXT_RPT_G,:CTL_BLK.TXT_BAL_G
      		FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      
      					 --#####
      			     SELECT sum(ACTUAL),sum(REPORTED) into :CTL_BLK.TXT_ACTUAL_G_TD ,:CTL_BLK.TXT_RPT_G_TD
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<=:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      			     --#####	
       	SELECT BALANCE INTO :Global.vBalance FROM DEMO.T_BF_PRODUCTION_TRACKING 
      			WHERE TIMESTAMP=(:CTL_BLK.TXT_TIMESTAMP_G)-1 AND FURNACE='G';	 
 			ELSE					

				Select SUM(NET_WT) into :CTL_BLK.TXT_ACTUAL_G  from  demo.t_ladle_details where
 						LADLE_FLEND_TIME>=:CTL_BLK.TXT_TIMESTAMP_G+6/24 and LADLE_FLEND_TIME<:CTL_BLK.TXT_TIMESTAMP_G+1+6/24 
							and DESTINATION<>'R' and fur_name='G';
			
				SELECT SUM(NVL(ACTUAL,0))-sum(NVL(REPORTED,0)) INTO :CTL_BLK.TXT_BAL_G
					FROM DEMO.T_BF_PRODUCTION_TRACKING 
						WHERE TIMESTAMP>=TRUNC(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G'; 			
			
		  	:CTL_BLK.TXT_RPT_G:=nvl(:CTL_BLK.TXT_ACTUAL_G,0)+nvl(:CTL_BLK.TXT_BAL_G,0);	
		  	:Global.vBalance:=:CTL_BLK.TXT_BAL_G;
				:CTL_BLK.TXT_BAL_G:=NVL(:CTL_BLK.TXT_ACTUAL_G,0)-NVL(:CTL_BLK.TXT_RPT_G,0)+NVL(:Global.vBalance,0);	
				
			         	--#####
								 vActual_TD:=0;
								 vReported_TD:=0;
      			     SELECT sum(ACTUAL),sum(REPORTED) into vActual_TD,vReported_TD 
      			     FROM DEMO.T_BF_PRODUCTION_TRACKING WHERE TIMESTAMP>=trunc(:CTL_BLK.TXT_TIMESTAMP_G,'MON') AND TIMESTAMP<:CTL_BLK.TXT_TIMESTAMP_G AND FURNACE='G';
      			     :CTL_BLK.TXT_ACTUAL_G_TD:=nvl(vActual_TD,0)+ nvl(:CTL_BLK.TXT_ACTUAL_G ,0);
      			     	:CTL_BLK.TXT_RPT_G_TD:=nvl(vReported_TD,0)+ nvl(:CTL_BLK.TXT_RPT_G ,0);      			     
      			     --#####	   		  			
 			END IF;
 	
		:CTL_BLK.DISPLAY_ACT_G:=nvl(:BLK_CONTROL.DISPLAY_ACTUAL,0)+nvl(:CTL_BLK.TXT_ACTUAL_G,0);
		:CTL_BLK.DISPLAY_RPT_G:=nvl(:BLK_CONTROL.DISPLAY_REPORTED,0)+nvl(:CTL_BLK.TXT_RPT_G,0);
		:CTL_BLK.DISPLAY_BAL_G:=nvl(:BLK_CONTROL.DISPLAY_BALANCE,0)+nvl(:CTL_BLK.TXT_BAL_G,0);
							
		--#####
		:CTL_BLK.DISPLAY_ACT_G_TD:=nvl(:BLK_CONTROL.DISPLAY_ACTUAL_TD,0)+nvl(:CTL_BLK.TXT_ACTUAL_G_TD,0);
		:CTL_BLK.DISPLAY_RPT_G_TD:=nvl(:BLK_CONTROL.DISPLAY_REPORTED_TD,0)+nvl(:CTL_BLK.TXT_RPT_G_TD,0);     			    
		--#####
		
									If :CTL_BLK.TXT_ACTUAL_G_TD=0 Then
      			     		:CTL_BLK.TXT_ACTUAL_G_TD:=Null;
      			     	End If;   
      			     	If :CTL_BLK.TXT_RPT_G_TD=0 Then
      			     		 :CTL_BLK.TXT_RPT_G_TD:=Null;
      			     	End If; 
