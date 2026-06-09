private decimal GetGrossWt(string trpNo, DateTime date, DateTime time, string from)
        {
              Select GROSS_WT into vGROSS_WT  From Demo.T_LADLE_DETAILS where FUR_NAME=vFUR and 
        TRP_NO=vTRPNO and  LADLE_FLEND_TIME=(Select Max(LADLE_FLEND_TIME) From  Demo.T_LADLE_DETAILS   where FUR_NAME=vFUR and TRP_NO=vTRPNO
          and LADLE_FLEND_TIME<=to_date(to_CHAR(vDATE,'DD-MON-YYYY')||to_char(vTime,'HH24:MI'),'DD-MON-YYYY HH24:MI'));         
          Return vGROSS_WT; 
        }
