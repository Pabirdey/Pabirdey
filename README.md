else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
{
    bool recordFound = false;

    using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();
        string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
        
        using (OracleCommand cmd = new OracleCommand(query, conn))
        {
            cmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo ?? "";
            cmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source ?? "";

            using (OracleDataReader reader = cmd.ExecuteReader())
            {
                if (reader.Read())
                {
                    recordFound = true;

                    model.PileNo = input.PileNo;
                    model.Source = input.Source;
                    model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                    model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                    model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                    model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                    model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                    model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                    model.YARD_FINES = reader["YARD_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["YARD_FINES"]);
                }
            }
        }
    }

    if (!recordFound)
    {
        ViewBag.Message = "No record exists for the given Pile No and Source.";
    }
}
