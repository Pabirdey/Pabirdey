RETURN_FINES = dr["RETURN_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["RETURN_FINES"]),
                                    WET_FINES = dr["WET_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["WET_FINES"]),
                                    DRY_FINES = dr["DRY_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES"]),
                                    DRY_FINES_500TPH = dr["DRY_FINES_500TPH"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES_500TPH"])
