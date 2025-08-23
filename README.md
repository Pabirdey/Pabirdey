@model YourNamespace.Models.RmbbPile
@{
    ViewBag.Title = "Raw Material Quantity";
}

<h4 class="mb-4" id="Main_Heading">Raw Material Quantity</h4>
<hr class="section-divider" />

@if (!string.IsNullOrEmpty(ViewBag.Message))
{
    <div class="alert alert-info">@ViewBag.Message</div>
}

@using (Html.BeginForm("RmbbPile", "YourControllerName", FormMethod.Post, new { id = "rawMaterialForm" }))
{
 <div class="form-group">
        <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary" />
    </div>

    @if (!string.IsNullOrEmpty(ViewBag.Message as string))
    {
        <div class="alert alert-info mt-2">
            @ViewBag.Message
        </div>
    }
}
  <div class="form-group row">
        <label class="col-sm-2 col-form-label">Source</label>
        <div class="col-sm-4">
            <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                <option value="">-- Select Source --</option>
                <option value="RMBB_KNR" @(Model?.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                <option value="RMBB" @(Model?.Source == "RMBB" ? "selected" : "")>RMBB</option>
                <option value="RMBBN" @(Model?.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
            </select>
        </div>
    </div>

    [HttpPost]
public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
{
    RmbbPile model = new RmbbPile();
    ViewBag.Message = "";

    if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            string checkSql = "SELECT COUNT(*) FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
            using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
            {
                checkCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                checkCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                int count = Convert.ToInt32(checkCmd.ExecuteScalar());

                if (!string.IsNullOrEmpty(SaveRawMaterial))
                {
                    if (count > 0)
                    {
                        // UPDATE
                        string updateSql = @"
                            UPDATE imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK SET
                                PREP_START_DATE = :PREP_START_DATE,
                                PREP_END_DATE   = :PREP_END_DATE,
                                CONS_ST_DATE    = :CONS_ST_DATE,
                                NOA_FINES       = :NOA_FINES,
                                JODA_FINES      = :JODA_FINES,
                                KB_FINES        = :KB_FINES,
                                YARD_FINES      = :YARD_FINES
                            WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";

                        using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                        {
                            updateCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;
                            updateCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                            updateCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                            updateCmd.ExecuteNonQuery();
                            ViewBag.Message = "Record updated successfully.";
                        }
                    }
                    else
                    {
                        // INSERT
                        string insertSql = @"
                            INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                            (PILE_NO, SOURCE, PREP_START_DATE, PREP_END_DATE, CONS_ST_DATE, NOA_FINES, JODA_FINES, KB_FINES, YARD_FINES)
                            VALUES (:PILE_NO, :SOURCE, :PREP_START_DATE, :PREP_END_DATE, :CONS_ST_DATE, :NOA_FINES, :JODA_FINES, :KB_FINES, :YARD_FINES)";

                        using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                        {
                            insertCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                            insertCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;
                            insertCmd.Parameters.Add(":PREP_START_DATE", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":PREP_END_DATE", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":CONS_ST_DATE", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                            insertCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;

                            insertCmd.ExecuteNonQuery();
                            ViewBag.Message = "Record inserted successfully.";
                        }
                    }

                    model = input; // Retain form data after save
                }
                else if (count > 0)
                {
                    // LOAD DATA FOR VIEW
                    string selectSql = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";
                    using (OracleCommand selectCmd = new OracleCommand(selectSql, conn))
                    {
                        selectCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                        selectCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

                        using (OracleDataReader reader = selectCmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
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
                else
                {
                    ViewBag.Message = "No data found for given Pile No and Source.";
                }
            }
        }
    }
    else
    {
        ViewBag.Message = "Please enter both Pile No and Source.";
    }

    return View(model);
}

