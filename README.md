	Select nvl(Max(CAST_NO),0)+1  ,nvl(Max(Seq_NO),0)+1 into maxCastno,v_seq_no  from imtg.T_GRANSHOT_DETAILS ;
