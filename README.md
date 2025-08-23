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
    <div class="container-fluid">

        <!-- Pile No and Source Selection -->
        <div class="d-flex flex-nowrap gap-2 align-items-end mb-3">
            <div style="width:8%;">
                <label class="form-label">Pile No</label>
                <input class="form-control" type="text" name="PileNo" value="@Model?.PileNo" required autocomplete="off" />
            </div>

            <div style="width:8%;">
                <label class="form-label">Select Source</label>
                <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                    <option value="">-- Select Source --</option>
                    <option value="RMBB_KNR" @(Model?.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                    <option value="RMBB" @(Model?.Source == "RMBB" ? "selected" : "")>RMBB</option>
                    <option value="RMBBN" @(Model?.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                </select>
            </div>

            <div style="width:8%">
                <label class="form-label">Shift</label>
                <select class="form-select">
                    <option value="A">A</option>
                    <option value="B">B</option>
                    <option value="C">C</option>
                </select>
            </div>

            <div style="width:12%;">
                <label class="form-label">Start Date</label>
                <input type="text" class="form-control" name="StartDate" id="StartDate"
                       value="@(Model?.StartDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>

            <div style="width:12%;">
                <label class="form-label">End Date</label>
                <input type="text" class="form-control" name="EndDate" id="EndDate"
                       value="@(Model?.EndDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>

            <div style="width:12%;">
                <label class="form-label">Cons.St.Date</label>
                <input type="text" class="form-control" name="ConsStartDate" id="ConsStartDate"
                       value="@(Model?.ConsStartDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>
        </div>

        <hr class="section-divider" />

        <!-- Material Inputs -->
        <div class="row material-row mb-3">
            <div class="col-md-2">
                <label class="form-label">Noa Fines</label>
                <input class="form-control" type="text" name="NOA_FINES" value="@Model?.NOA_FINES" />
            </div>
            <div class="col-md-2">
                <label class="form-label">Joda Fines</label>
                <input class="form-control" type="text" name="JODA_FINES" value="@Model?.JODA_FINES" />
            </div>
            <div class="col-md-2">
                <label class="form-label">KB Fines</label>
                <input class="form-control" type="text" name="KB_FINES" value="@Model?.KB_FINES" />
            </div>
            <div class="col-md-2">
                <label class="form-label">Yard Fines</label>
                <input class="form-control" type="text" name="YARD_FINES" value="@Model?.YARD_FINES" />
            </div>
            <div class="col-md-2">
                <label class="form-label">BHJ</label>
                <input class="form-control" type="text" name="TXT_BHJ" value="@Model?.TXT_BHJ" />
            </div>
            <div class="col-md-2">
                <label class="form-label">Namisa</label>
                <input class="form-control" type="text" name="IO_NAMISA" value="@Model?.IO_NAMISA" />
            </div>
        </div>

        <!-- Save Button -->
        <div class="form-group mt-3">
            <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary" />
        </div>

        <!-- Optional message again -->
        @if (!string.IsNullOrEmpty(ViewBag.Message as string))
        {
            <div class="alert alert-info mt-2">
                @ViewBag.Message
            </div>
        }
    </div>
}
[HttpPost]
public ActionResult RmbbPile(RmbbPile input, string SaveRawMaterial)
{
    RmbbPile model = new RmbbPile();
    ViewBag.Message = "";

    if (string.IsNullOrEmpty(input.PileNo) || string.IsNullOrEmpty(input.Source))
    {
        ViewBag.Message = "Please enter both Pile No and Source.";
        return View(input);
    }

    using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();

        string checkSql = @"SELECT COUNT(*) FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                            WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";

        using (OracleCommand checkCmd = new OracleCommand(checkSql, conn))
        {
            checkCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
            checkCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;

            int recordExists = Convert.ToInt32(checkCmd.ExecuteScalar());

            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {
                // === INSERT OR UPDATE ===
                if (recordExists > 0)
                {
                    // === UPDATE ===
                    string updateSql = @"
                        UPDATE imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK SET
                            PREP_START_DATE = :StartDate,
                            PREP_END_DATE   = :EndDate,
                            CONS_ST_DATE    = :ConsStartDate,
                            NOA_FINES       = :NOA_FINES,
                            JODA_FINES      = :JODA_FINES,
                            KB_FINES        = :KB_FINES,
                            YARD_FINES      = :YARD_FINES
                        WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";

                    using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                    {
                        updateCmd.Parameters.Add(":StartDate", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        updateCmd.Parameters.Add(":ConsStartDate", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
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
                    // === INSERT ===
                    string insertSql = @"
                        INSERT INTO imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                        (PILE_NO, SOURCE, PREP_START_DATE, PREP_END_DATE, CONS_ST_DATE, NOA_FINES, JODA_FINES, KB_FINES, YARD_FINES)
                        VALUES 
                        (:PILE_NO, :SOURCE, :StartDate, :EndDate, :ConsStartDate, :NOA_FINES, :JODA_FINES, :KB_FINES, :YARD_FINES)";

                    using (OracleCommand insertCmd = new OracleCommand(insertSql, conn))
                    {
                        insertCmd.Parameters.Add(":PILE_NO", OracleDbType.Varchar2).Value = input.PileNo;
                        insertCmd.Parameters.Add(":SOURCE", OracleDbType.Varchar2).Value = input.Source;
                        insertCmd.Parameters.Add(":StartDate", OracleDbType.Date).Value = input.StartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":EndDate", OracleDbType.Date).Value = input.EndDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":ConsStartDate", OracleDbType.Date).Value = input.ConsStartDate ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":NOA_FINES", OracleDbType.Decimal).Value = input.NOA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":JODA_FINES", OracleDbType.Decimal).Value = input.JODA_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":KB_FINES", OracleDbType.Decimal).Value = input.KB_FINES ?? (object)DBNull.Value;
                        insertCmd.Parameters.Add(":YARD_FINES", OracleDbType.Decimal).Value = input.YARD_FINES ?? (object)DBNull.Value;

                        insertCmd.ExecuteNonQuery();
                        ViewBag.Message = "Record inserted successfully.";
                    }
                }

                model = input; // Retain form values after Save
            }
            else if (recordExists > 0)
            {
                // === LOAD EXISTING DATA ===
                string selectSql = @"SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW_BK 
                                     WHERE PILE_NO = :PILE_NO AND SOURCE = :SOURCE";

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
                            model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                            model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                            model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                            model.NOA_FINES = reader["NOA_FINES"] == DBNull.Value ? null : Convert.ToDecimal(reader["NOA_FINES"]);
                            model.JODA_FINES = reader["JODA_FINES"] == DBNull.Value ? null : Convert.ToDecimal(reader["JODA_FINES"]);
                            model.KB_FINES = reader["KB_FINES"] == DBNull.Value ? null : Convert.ToDecimal(reader["KB_FINES"]);
                            model.YARD_FINES = reader["YARD_FINES"] == DBNull.Value ? null : Convert.ToDecimal(reader["YARD_FINES"]);
                        }
                    }
                }
            }
            else
            {
                ViewBag.Message = "No data found for this Pile No and Source.";
                model.PileNo = input.PileNo;
                model.Source = input.Source;
            }
        }
    }

    return View(model);
}
