    v_days:=288*(to_number(to_date(to_char(Sysdate,'DD-MON-YYYY HH24:MI:SS'),'DD-MON-YYYY HH24:MI:SS')-to_date(to_char(vMAXDATE,'DD-MON-YYYY HH24:MI:SS'),'DD-MON-YYYY HH24:MI:SS')));
     For v_count in 1..v_days
    Loop
        Insert into imtg.T_JODA_IOPP_PROCESS_RAW
        (
          Timestamp         
          
          )
          values  (to_date(to_char(vMAXDATE,'DD-MON-YYYY HH24:MI:SS'),'DD-MON-YYYY HH24:MI:SS'));      
           vMAXDATE :=((to_date(to_char(vMAXDATE,'DD-MON-YYYY HH24:MI:SS'),'DD-MON-YYYY HH24:MI:SS')+1/288));
	 End loop;
     commit;
