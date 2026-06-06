Declare 
	vcount number;		
Begin
 	  If :T_LADLE_MASTER.TXTDT is Not Null and :T_LADLE_MASTER.TXTSHIFT is Not Null AND :T_LADLE_MASTER.TXTFUR  is not null Then
				Select count(*) into vcount from IMTG.T_GRANSHOT_DETAILS where TIMESTAMP=:T_LADLE_MASTER.TXTDT And SHIFT=:T_LADLE_MASTER.TXTSHIFT  and AREA=:T_LADLE_MASTER.TXTFUR;
				If vCount>0 Then
						GO_Block('T_LADLE_DETAILS');
						CLEAR_BLOCK();
						FIRST_RECORD;
						For i in (Select * from IMTG.T_GRANSHOT_DETAILS
						where TIMESTAMP=:T_LADLE_MASTER.TXTDT And SHIFT=:T_LADLE_MASTER.TXTSHIFT  and AREA=:T_LADLE_MASTER.TXTFUR Order by CAST_NO)
						Loop
							:T_LADLE_DETAILS.CAST_NO:=i.CAST_NO;
							:T_LADLE_DETAILS.CAST_ST_TIME:=i.CAST_ST_TIME;
							:T_LADLE_DETAILS.CAST_END_TIME:=i.CAST_END_TIME;
							:T_LADLE_DETAILS.TRP_NO:=i.TRP_NO;
							:T_LADLE_DETAILS.LADLE_FLST_TIME:=i.LADLE_FLST_TIME;
							:T_LADLE_DETAILS.LADLE_FLEND_TIME:=i. LADLE_FLEND_TIME;
							:T_LADLE_DETAILS.ARRIVED_FROM:=i.ARRIVED_FROM;
							:T_LADLE_DETAILS.GROSS_WT:=i.GROSS_WT;
							:T_LADLE_DETAILS.TARE_WT:=i.TARE_WT;
							:T_LADLE_DETAILS.NET_WT:=i.NET_WT;
							:T_LADLE_DETAILS.HMT:=i.HMT;
							:T_LADLE_DETAILS.TXT_LADLEFILLINGRATE:=i.POURING_RATE;
							:T_LADLE_DETAILS.TXT_RFO:=i.REASON_POURING;																																																																																																																																																																																																																																						
							:T_LADLE_DETAILS.SEQ_NO:=i.SEQ_NO;
							NEXT_RECORD;
						End Loop;
						FIRST_RECORD;							
				End If;
			
			
End If;
go_item('T_LADLE_MASTER.EXIT');
Exception
When Others Then Null;  
End;
  <div class="table-container">
                                <table class="table table-bordered text-center">
                                    <thead>
                                        <tr>
                                            <th>CastNo</th>
                                            <th>Start</th>
                                            <th>End</th>
                                            <th>Ladle No</th>
                                            <th>Start</th>
                                            <th>End</th>
                                            <th>Arrived From</th>
                                            <th>Gross</th>
                                            <th>Tare</th>
                                            <th>Net</th>
                                            <th>Pouring Rate</th>
                                            <th>HMT</th>
                                            <th>Reason For Outage</th>
                                            <th>Seq_No</th>
                                            <th>Delete</th>
                                        </tr>
                                    </thead>
                                    <tbody id="tblBody">
                                      <tr></tr>
                                    </tbody>
                                </table>
                            </div>     
