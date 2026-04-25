RETURN_FINES = dr["RETURN_FINES"] == DBNull.Value 
               ? null 
               : (decimal?)Convert.ToDecimal(dr["RETURN_FINES"]);
