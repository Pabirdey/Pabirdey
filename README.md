cmd.Parameters.Add("P_EndDate",OracleDbType.Decimal).Value=input.PREP_END_DATE??"";
cmd.Parameters.Add("P_ConstStartDate",OracleDbType.Decimal).Value=input.CONS_ST_DATE??"";
cmd.Parameters.Add("P_NoaFines",OracleDbType.Decimal).Value=input.NOA_FINES  ??"";
cmd.Parameters.Add("P_JodaFines",OracleDbType.Decimal).Value=input.JODA_FINES??"";
cmd.Parameters.Add("P_KBFines",OracleDbType.Decimal).Value=input.KB_FINES??"";
