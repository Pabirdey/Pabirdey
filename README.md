cmd.Parameters.Add(":CLOSURE_MODE",
    row.IsNull("CLOSURE_MODE") ? (object)DBNull.Value : row["CLOSURE_MODE"]);

cmd.Parameters.Add(":CLAY_QUANTITY",
    row.IsNull("CLAY_QUANTITY") ? (object)DBNull.Value : row["CLAY_QUANTITY"]);

cmd.Parameters.Add(":CLAY_QTY_USED",
    row.IsNull("CLAY_QTY_USED") ? (object)DBNull.Value : row["CLAY_QTY_USED"]);