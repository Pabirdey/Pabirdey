TIMESTAMP = dr["TIMESTAMP"] == DBNull.Value 
            ? (DateTime?)null 
            : (DateTime?)dr.GetDateTime(dr.GetOrdinal("TIMESTAMP")),
