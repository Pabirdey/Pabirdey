cmd.Parameters.Add(":CLOSURE_MODE",
    row["CLOSURE_MODE"] == DBNull.Value ? (object)DBNull.Value : row["CLOSURE_MODE"]);

cmd.Parameters.Add(":CLAY_QUANTITY",
    row["CLAY_QUANTITY"] == DBNull.Value ? (object)DBNull.Value : row["CLAY_QUANTITY"]);

cmd.Parameters.Add(":CLAY_QTY_USED",
    row["CLAY_QTY_USED"] == DBNull.Value ? (object)DBNull.Value : row["CLAY_QTY_USED"]);


cmd.Parameters.Add(new OracleParameter(":CLOSURE_MODE",
    row["CLOSURE_MODE"] == DBNull.Value
        ? (object)DBNull.Value
        : row["CLOSURE_MODE"]));

cmd.Parameters.Add(new OracleParameter(":CLAY_QUANTITY",
    row["CLAY_QUANTITY"] == DBNull.Value
        ? (object)DBNull.Value
        : row["CLAY_QUANTITY"]));

cmd.Parameters.Add(new OracleParameter(":CLAY_QTY_USED",
    row["CLAY_QTY_USED"] == DBNull.Value
        ? (object)DBNull.Value
        : row["CLAY_QTY_USED"]));