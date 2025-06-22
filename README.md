.Open();

                    using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;
                        cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                        cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                        cmd.Parameters.Add("P_EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        cmd.Parameters.Add("P_ConstStartDate",OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? (object)DBNull.Value;
                        cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? (object)DBNull.Value; cmd.ExecuteNonQuery();
}
create or replace PROCEDURE Proc_Save_Pile_Rawmat_Quantity_Entry (
    P_PileNo     IN VARCHAR2,
    P_Source     IN VARCHAR2,
    P_StartDate  IN DATE Default Null,    
    P_EndDate    IN DATE Default Null,
    P_ConstStartDate IN DATE Default Null,
    P_NoaFines	IN Number Default NULL,
    P_JodaFines	IN Number Default NULL,
    P_KBFines	IN Number Default NULL
    )
AS
vCOUNT Number;
BEGIN
   EXECUTE IMMEDIATE 'ALTER SESSION SET NLS_DATE_FORMAT=''DD-MON-YYYY HH24:MI:SS''';
   Select COUNT(*) into vCOUNT From imtg.T_PILE_RAWMAT_QUANTITY_NEW Where PILE_NO=P_PileNo and SOURCE=P_Source;  
   If vCOUNT=0 Then 
   Insert into imtg.T_PILE_RAWMAT_QUANTITY_NEW(PILE_NO,SOURCE,PREP_START_DATE,PREP_END_DATE,CONS_ST_DATE,NOA_FINES,JODA_FINES)
    Values(P_PileNo,P_Source,P_StartDate  ,P_EndDate,P_ConstStartDate ,P_NoaFines,P_JodaFines);	
   Else
    Update imtg.T_PILE_RAWMAT_QUANTITY_NEW
    SET
            PREP_START_DATE=P_StartDate  ,
            PREP_END_DATE=P_EndDate    ,
            CONS_ST_DATE=P_ConstStartDate ,
            NOA_FINES=P_NoaFines,
            JODA_FINES=P_JodaFines

                Where pile_no=P_PileNo AND source=P_Source;
   End If;   
commit;
EXCEPTION
WHEN OTHERS THEN
DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;


    
                        
