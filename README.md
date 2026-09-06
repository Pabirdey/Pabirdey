model.TLC_ST_DATE = dr["TLC_ST_DATE"] == DBNull.Value
    ? (DateTime?)null
    : Convert.ToDateTime(dr["TLC_ST_DATE"]);

model.TLC_END_DATE = dr["TLC_END_DATE"] == DBNull.Value
    ? (DateTime?)null
    : Convert.ToDateTime(dr["TLC_END_DATE"]);
